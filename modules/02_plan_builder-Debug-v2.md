for day in trip_days:
  prior_themes = []

  morning = pick activity(
    candidates.filter(open_in(morning_window))
              .filter(proximity(lodging, ≤20min))
              .filter(fits_slot(morning_window))
  )
  prior_themes.append(morning.theme)

  midday = pick activity(
    candidates.filter(open_in(midday_window))
              .filter(proximity(morning, ≤20min))
              .filter(fits_slot(midday_window))
  )
  prior_themes.append(midday.theme)

  afternoon = pick activity(
    candidates.filter(open_in(afternoon_window))
              .filter(proximity(midday, ≤35min))
              .filter(theme_different(prior_themes))
              .filter(fits_slot(afternoon_window))
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
