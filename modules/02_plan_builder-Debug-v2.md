for day in trip_days:
  prior themes = []

  morning = pick activity(eg:
    candidates.filter(open_in(morning window))
              .filter(proximity(lodging, ≤20min))
              .filter(fits slot(morning window))
  )
  prior themes.append(morning.theme)

  midday = pick activity(
    candidates.filter(open in(midday window))
              .filter(proximity(morning, ≤20min))
              .filter(fits slot(midday window))
  )
  prior_themes.append(midday.theme)

  afternoon = pick activity(
    candidates.filter(open in(afternoon_window))
              .filter(proximity(midday, ≤35min))
              .filter(theme different(prior themes))
              .filter(fits slot(afternoon window))
  )
  prior themes.append(afternoon.theme)

  evening = pick_restaurant_or_event(
    candidates_restaurants.filter(open_in(evening_window))
                          .filter(proximity(afternoon, ≤35min))
                          .filter(fits_slot(evening_window))
  )

  if any_slot_missing:
    apply_fallbacks(day_context)

  day_output = summarize_day(morning, midday, afternoon, evening)
