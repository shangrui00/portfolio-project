import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class CalendarEventManager {
    private Map<String, List<String>> events;

    public CalendarEventManager() {
        this.events = new HashMap<>();
    }

    /**
     * Adds an event to the specified date.
     * @param name The name of the event.
     * @param date The date (in YYYY-MM-DD format).
     * @param time The time (in HH:MM AM/PM format).
     */
    public void addEvent(String name, String date, String time) {
        String eventDetails = name + " at " + time;
        events.computeIfAbsent(date, k -> new ArrayList<>()).add(eventDetails);
    }

    /**
     * Removes an event by its name.
     * @param name The name of the event.
     */
    public void removeEvent(String name) {
        for (List<String> eventList : events.values()) {
            eventList.removeIf(event -> event.contains(name));
        }
    }

    /**
     * Retrieves the list of events for a specific date.
     * @param date The date (in YYYY-MM-DD format).
     * @return A list of events, or an empty list if no events are found.
     */
    public List<String> getDate(String date) {
        return events.getOrDefault(date, new ArrayList<>());
    }

    /**
     * Checks if an event with the given name exists.
     * @param eventName The name of the event.
     * @return true if the event exists, false otherwise.
     */
    public boolean hasEvent(String eventName) {
        for (List<String> eventList : events.values()) {
            for (String event : eventList) {
                if (event.contains(eventName)) {
                    return true;
                }
            }
        }
        return false;
    }

    /**
     * Gets the number of events on a specific date.
     * @param date The date (in YYYY-MM-DD format).
     * @return The number of events on that date.
     */
    public int getCountOnDate(String date) {
        return events.getOrDefault(date, new ArrayList<>()).size();
    }

    public static void main(String[] args) {
        CalendarEventManager manager = new CalendarEventManager();

        // Add some events
        manager.addEvent("Doctor Appointment", "2024-10-15", "10:00 AM");
        manager.addEvent("Meeting with Team", "2024-10-15", "2:00 PM");
        manager.addEvent("Lunch with Friend", "2024-10-16", "12:30 PM");

        // Retrieve events for a specific date
        System.out.println("Events on 2024-10-15: " + manager.getDate("2024-10-15"));

        // Check if a specific event exists
        System.out.println("Has event 'Doctor Appointment': " + manager.hasEvent("Doctor Appointment"));

        // Get the number of events on a specific date
        System.out.println("Number of events on 2024-10-15: " + manager.getCountOnDate("2024-10-15"));

        // Remove an event
        manager.removeEvent("Meeting with Team");
        System.out.println("Events on 2024-10-15 after removal: " + manager.getDate("2024-10-15"));
    }
}
