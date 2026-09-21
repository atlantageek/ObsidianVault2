Item 2 (**Expected Optical Power Calculator**) is actually one of the most straightforward features because your fiber data model already contains most of the required information.

The core idea is:

> Given a point in the network, estimate what optical power should be measured there if the network is healthy.

Then compare that estimate to the actual field measurement.

---

# What You Need
 
Your fiber model already tracks:

- OLTs
    
- Fibers
    
- Splices
    
- Splitters
    
- ONTs/ONUs
    

You simply need to add loss calculations.

---

# Build a Loss Budget Engine

Each component contributes loss.

## Fiber Loss

Typical GPON values:

|Fiber Type|Loss|
|---|---|
|1310nm|0.35 dB/km|
|1490nm|0.25 dB/km|
|1550nm|0.20 dB/km|

Example:

2.5 km fiber

1490nm:

```
2.5 * 0.25 = 0.625 dB
```

---

## Splice Loss

Typical:

```
0.05 dB to 0.1 dB
```

Use:

```
0.1 dB
```

until measured values exist.

---

## Connector Loss

Typical:

```
0.3 dB to 0.5 dB
```

Use:

```
0.5 dB
```

---

## Splitter Loss

The big one.

Typical values:

|Split Ratio|Loss|
|---|---|
|1:2|3.5 dB|
|1:4|7.2 dB|
|1:8|10.5 dB|
|1:16|13.5 dB|
|1:32|17 dB|
|1:64|20.5 dB|

Store these in a lookup table.

---

# Traverse the Topology

Suppose a technician selects an ONT.

You already know the path:

```
OLT
→ feeder fiber
→ splice
→ splitter
→ splice
→ distribution fiber
→ ONT
```

Walk the graph and accumulate loss.

Pseudo-code:

```csharp
double totalLoss = 0;

foreach(var component in path)
{
    switch(component.Type)
    {
        case Fiber:
            totalLoss += component.LengthKm * 0.25;
            break;

        case Splice:
            totalLoss += 0.1;
            break;

        case Connector:
            totalLoss += 0.5;
            break;

        case Splitter:
            totalLoss += splitterLoss[component.Ratio];
            break;
    }
}
```

---

# Calculate Expected Power

Assume:

OLT transmit power:

```
+4 dBm
```

Total loss:

```
22.3 dB
```

Expected ONT receive power:

```
4 - 22.3
=
-18.3 dBm
```

---

# Build an Expected Range

Don't show a single value.

Show:

```
Expected:
-17 to -20 dBm
```

because:

- splice variation
    
- connector variation
    
- manufacturing tolerances
    

exist.

A ±1.5 dB band is usually reasonable.

---

# Where This Gets Interesting

Most systems stop there.

Your topology lets you do more.

---

## Expected Power at Any Point

Technician standing at:

- FDH
    
- Cabinet
    
- Handhole
    
- Splitter output
    

AI can estimate power there too.

Example:

```
Expected at splitter input:
+1.5 dBm

Expected at splitter output:
-15.5 dBm
```

Very useful for troubleshooting.

---

# Branch Comparison

This is where your existing topology becomes valuable.

Suppose:

Splitter outputs:

|Branch|Measured|
|---|---|
|1|-21|
|2|-22|
|3|-21|
|4|-28|

AI immediately knows:

```
Branch 4 abnormal
```

Even if the absolute budget isn't perfect.

This often catches issues faster than budget calculations.

---

# Fault Estimation

Once you have expected power:

### Scenario A

Expected:

```
-21 dBm
```

Measured:

```
-22 dBm
```

AI:

```
Normal
```

---

### Scenario B

Expected:

```
-21 dBm
```

Measured:

```
-28 dBm
```

AI:

```
Excess loss = 7 dB
```

Now estimate likely causes:

|Cause|Typical Loss|
|---|---|
|Dirty connector|1-3 dB|
|Bad splice|1-5 dB|
|Macro bend|2-10 dB|
|Crushed drop|3-15 dB|

---

# Next-Level Version

Because you already map the network, calculate cumulative loss at every node.

Store:

```sql
network_node_loss
-----------------
node_id
loss_from_olt
expected_power
```

Whenever topology changes:

- recompute once
    
- cache results
    

Then technician lookups become instant.

No graph traversal during troubleshooting.

---

# The Executive Pitch

This feature turns your fiber inventory from a documentation system into an operational tool.

Instead of showing:

> "This customer is connected to Splitter S-14"

the system can tell a technician:

> "Expected receive power at this ONT is -19 dBm. Current measured power is -26 dBm. Excess loss of 7 dB detected. Similar customers on the same splitter are within normal range. Probable issue is between splitter output and customer premises."

That's the point where the fiber map begins actively helping technicians solve problems rather than simply displaying network assets.