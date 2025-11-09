# Week 2 Report — AI Green Transportation (Bangalore)

## 1️⃣ Objective
Develop a real-time, emission-optimized route planning system using **real road data from Bangalore (India)**.  
This week’s goal: implement data preprocessing, route optimization (shortest vs least-emission), and visualization using OpenStreetMap (OSMnx).

---

## 2️⃣ Data & Environment
- **City:** Bangalore, India  
- **Source:** OpenStreetMap via OSMnx (`network_type='drive'`)  
- **Nodes:** ~154,000 | **Edges:** ~391,000  
- **Base vehicle type:** Petrol Car  
- **Emission Factor:** 192 g CO₂ per km  
- **Tools Used:** Python (OSMnx, NetworkX, Pandas, GeoPandas, Folium, Matplotlib)  
- **Files Generated:**
  - `data/real_routes_bangalore.csv`
  - `data/optimized_route_bangalore.json`
  - `visualizations/optimized_real_route_bangalore.html`
  - `visualizations/compare_routes_bangalore.html`
  - `visualizations/summary_comparison.png`

---

## 3️⃣ Methodology (Step-by-Step)

### 📍 Step 1: Real Map Data Extraction
Used:
```python
G = ox.graph_from_place("Bangalore, India", network_type="drive")



to download the drivable road network.

⚙️ Step 2: Data Preprocessing

Converted the graph to GeoDataFrames using ox.graph_to_gdfs().

Calculated distance (km), travel time (min), and estimated max speed (km/h).

Handled missing speed data by setting default = 40 km/h.

🌱 Step 3: Emission Computation

Assigned base emission factor = 192 g CO₂/km (Petrol Car).

Applied road-type multipliers:

Motorway = 0.7, Primary = 0.9, Residential = 1.2, Service = 1.3

Applied speed factor = 40 / maxspeed to simulate higher emissions on slower roads.

🧭 Step 4: Route Optimization

Used Dijkstra’s shortest path algorithm twice:

Least Emission Route: weight='emission_gCO2'

Shortest Distance Route: weight='distance_km'

🗺️ Step 5: Visualization

Visualized both routes using Folium:

Green = Emission-Optimized Route

Red = Shortest-Distance Route
Interactive maps saved as:

optimized_real_route_bangalore.html

compare_routes_bangalore.html

4️⃣ Results Summary
Metric	Emission-Optimized Route	Shortest-Distance Route
Distance (km)	11.01	10.84
CO₂ Emission (g)	1975.01	1998.66
Time (min)	16.52	16.26
Emission Reduction (%)	1.18%	—

Notebook Output:

🌿 Emission-Optimized Route:
   Distance: 11.01 km | Emission: 1975.01 g CO₂ | Time: 16.52 min
🚗 Shortest-Distance Route:
   Distance: 10.84 km | Emission: 1998.66 g CO₂ | Time: 16.26 min
💚 Emission Reduction: 1.18%

5️⃣ Visualizations
🗺️ 1. Emission-Optimized Route

🟥🟩 2. Comparison of Both Routes

📊 3. Emission & Distance Comparison Chart

6️⃣ Insights & Analysis

✅ The emission-optimized route took a slightly longer but cleaner path, preferring highways and avoiding local roads.
✅ Achieved 1.18% emission reduction compared to the shortest-distance route.
✅ Demonstrates that small routing optimizations can reduce emissions without major time penalties.
✅ The difference is clearer over longer distances or when diverse road types exist.

7️⃣ Limitations

Only one vehicle type (Petrol Car) used — fixed emission rate.

Real-time traffic not yet included.

No API-based live speed or congestion data.

Emission difference is smaller for shorter intra-city routes (due to similar road classes).

8️⃣ Next Steps (Week 3 Plan)

Add multiple vehicle types — Car, Bike, Bus, EV with distinct emission factors.

Integrate live traffic data (Google Maps / HERE API).

Build a Streamlit dashboard for easy user interaction.

Include emission savings summary in real time for users.

9️⃣ References

OpenStreetMap via OSMnx

European Environment Agency (EEA) CO₂ emission factors

NetworkX (Dijkstra algorithm for route optimization)

🔟 Acknowledgement

This report is part of the AI Green Transportation Project, focused on leveraging AI and open data for sustainable urban mobility.