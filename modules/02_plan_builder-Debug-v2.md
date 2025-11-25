# Module 2 — Plan Builder (Options → Days)
## Inputs
- **Lodging details**: location, check-in/out times, default transport mode  
- **Activities list**: type, theme, duration, open hours, cost range, location, reservation requirement  
- **Constraints**: trip dates, daily/overall budget, user preferences (themes, pace, dietary needs)
- **Transit assumptions**: walking speed, public transit averages, rideshare estimates, buffer allowances

## Time Slots
- **Morning (09:00–12:00)** → activity near lodging (≤20 min travel)  
- **Midday (12:00–15:00)** → activity close to morning slot (≤20 min travel)  
- **Afternoon (15:00–18:00)** → activity with a different theme (≤35 min travel)  
- **Evening (18:00–21:00)** → restaurant or optional event (≤35 min travel)  

*Include travel buffers (15–30 min) and allow ±30 min flexibility per slot.*

## Selection Rules
1. **Feasibility** → activity must fit slot duration + travel + buffer, and align with open hours  
2. **Proximity** → morning near lodging, midday near morning, afternoon broader radius, evening near afternoon or lodging  
3. **Theme diversity** → afternoon must differ from earlier slots (food, culture, nature, shopping, entertainment)  
4. **Budget compliance** → daily costs must stay within user’s budget  
5. **Preferences** → reflect user interests and dietary needs  
6. **Reservations** → flag activities requiring booking and note “reserve ahead”

## Edge Cases
- **Missing data** → assume defaults (duration 60–90 min, if cost unknown suggested another activity, mark “check availability”)  
- **Budget limits** → prioritize free options (parks, walks, viewpoints, free museums); mark paid items 
- **Overbooked day** → leave slot open intentionally as “rest time”

## Output (Per Day)
Each day’s plan is presented in a structured format:

- **Morning** → activity, type, theme, duration, cost, distance from lodging  
- **Midday** → activity, type, theme, duration, cost, proximity to morning  
- **Afternoon** → activity, type, theme, duration, cost, note on theme variety  
- **Evening** → restaurant/event, cuisine/type, reservation flag, cost, distance  
- **Totals** → estimated daily cost range, total travel time, notes (weather, reservations)


