# portfolio-project
Component Proof of Concept

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class CalendarEventManager {
    private Map<String, List<String>> events;

    public CalendarEventManager() {
        this.events = new HashMap<>();
    }

    public void addEvent(String name, String date, String time) {
        String eventDetails = name + " at " + time;
        events.computeIfAbsent(date, k -> new ArrayList<>()).add(eventDetails);
    }

    public void removeEvent(String name) {
        for (List<String> eventList : events.values()) {
            eventList.removeIf(event -> event.contains(name));
        }
    }

    public List<String> getDate(String date) {
        return events.getOrDefault(date, new ArrayList<>());
    }

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

    public int getCountOnDate(String date) {
        return events.getOrDefault(date, new ArrayList<>()).size();
    }

    public static void main(String[] args) {
        CalendarEventManager manager = new CalendarEventManager();

        manager.addEvent("Doctor Appointment", "2024-10-15", "10:00 AM");
        manager.addEvent("Meeting with Team", "2024-10-15", "2:00 PM");
        manager.addEvent("Lunch with Friend", "2024-10-16", "12:30 PM");

        System.out.println("Events on 2024-10-15: " + manager.getDate("2024-10-15"));

        System.out.println("Has event 'Doctor Appointment': " + manager.hasEvent("Doctor Appointment"));

        System.out.println("Number of events on 2024-10-15: " + manager.getCountOnDate("2024-10-15"));

        manager.removeEvent("Meeting with Team");
        System.out.println("Events on 2024-10-15 after removal: " + manager.getDate("2024-10-15"));
    }
}