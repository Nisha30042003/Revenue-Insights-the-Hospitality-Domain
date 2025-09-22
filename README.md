# Revenue Analytics Dashboard – Power BI Project

## Overview
This dashboard analyzes hotel performance across multiple cities and room types, focusing on revenue generation, occupancy trends, booking platforms, and weekly performance. It enables dynamic filtering and supports strategic decision-making through granular KPIs and visual storytelling.

---

## Metrics & DAX Formulas

###  Revenue
```DAX
Revenue = SUM('Bookings'[BookingAmount])
```
### Occupancy %
```DAX
Occupancy% = DIVIDE(SUM('Bookings'[OccupiedRooms]), SUM('Rooms'[AvailableRooms])) * 100
```
###  ADR (Average Daily Rate)
```DAX
ADR = DIVIDE(SUM('Bookings'[BookingAmount]), SUM('Bookings'[OccupiedRooms]))
```
###  RevPAR (Revenue per Available Room)
```DAX
RevPAR = DIVIDE(SUM('Bookings'[BookingAmount]), SUM('Rooms'[AvailableRooms]))
-- or --
RevPAR = ADR * (Occupancy% / 100)
```
###  Realisation %
```DAX
Realisation% = DIVIDE(SUM('Bookings'[BookingAmount]), SUM('Bookings'[ExpectedRevenue])) * 100
```
### Week-on-Week Change
```DAX
WoW Change = DIVIDE([CurrentWeekValue] - [PreviousWeekValue], [PreviousWeekValue]) * 100
``` 
### DSRN / DBRN / DURN 
```DAX
DSRN = CALCULATE(COUNTROWS('Bookings'), 'Bookings'[Source] = "Direct")
DBRN = COUNTROWS('Bookings')
DURN = CALCULATE(COUNTROWS('Bookings'), 'Bookings'[Status] = "Used")
``` 
###  Cancellation %
```DAX
CancelLation% = DIVIDE(COUNTROWS(FILTER('Bookings', 'Bookings'[Status] = "Canceled")), COUNTROWS('Bookings')) * 100
``` 
### Average Rating
```DAX
Average Rating = AVERAGE('Feedback'[Rating])
```
### Dashboard Layout

- **Filters**:  
  City and Room Type slicers for dynamic segmentation.

- **Time Series**:  
  Weekly trends for RevPAR, ADR, and Occupancy%, enabling temporal performance tracking.

- **Platform Analysis**:  
  Realisation% and ADR comparison across booking platforms (e.g., Tripster, Logtrip).

- **Category Breakdown**:  
  Occupancy% split by Business vs Luxury room segments to assess category-level performance.

- **Property-Level Table**:  
  Tabular view of revenue, average ratings, cancellations, and booking counts per hotel.

- **Comparative Trends**:  
  Week-on-week performance indicators to monitor growth, decline, and seasonal shifts.

### Insights Gained

- 🟢 **Tripster consistently outperforms other platforms** in ADR and Realisation%, indicating stronger monetization and customer loyalty.
- 🟡 **Luxury rooms show higher ADR but lower Occupancy%**, suggesting pricing optimization opportunities.
- 🔴 **Week 3 saw a spike in cancellations**, especially in City B, likely due to seasonal factors or platform issues.
- 🟢 **Direct bookings (DSRN) have higher Realisation%**, reinforcing the value of reducing platform dependency.
- 🟢 **City A maintains the highest RevPAR**, driven by balanced occupancy and pricing strategy.
- 🟢 **Customer ratings correlate positively with Realisation%**, highlighting the impact of service quality on revenue.

### Data Sources

- **Booking transactions**  
  Raw data capturing customer reservations, booking amounts, and timestamps.

- **Room availability logs**  
  Daily records of available vs occupied rooms across properties.

- **Customer feedback**  
  Ratings and reviews used to assess service quality and satisfaction.

- **Platform metadata**  
  Information about booking sources (e.g., Tripster, Logtrip), used for channel performance analysis.

  ### Use Cases

- **Revenue forecasting**  
  Predict future earnings based on historical booking and occupancy trends.

- **Operational efficiency tracking**  
  Monitor room utilization, cancellations, and service quality to optimize workflows.

- **Platform performance benchmarking**  
  Compare ADR, Realisation%, and booking volume across different platforms.

- **Strategic pricing and occupancy planning**  
  Align room rates and availability with demand patterns to maximize RevPAR.






