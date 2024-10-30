from datetime import datetime, timedelta

class VacationPlanner:
    def __init__(self):
        self.itinerary = {}
        self.destination = ""
        self.start_date = None
        self.end_date = None

    def set_trip_details(self):
        self.destination = input("Enter vacation destination: ")
        start_date_str = input("Enter start date (YYYY-MM-DD): ")
        end_date_str = input("Enter end date (YYYY-MM-DD): ")
        
        self.start_date = datetime.strptime(start_date_str, "%Y-%m-%d")
        self.end_date = datetime.strptime(end_date_str, "%Y-%m-%d")

    def add_activity(self):
        date_str = input("Enter date for activity (YYYY-MM-DD): ")
        date = datetime.strptime(date_str, "%Y-%m-%d")
        
        if date < self.start_date or date > self.end_date:
            print("Date is outside of vacation period!")
            return

        time = input("Enter time (HH:MM): ")
        activity = input("Enter activity description: ")
        location = input("Enter location: ")
        
        if date_str not in self.itinerary:
            self.itinerary[date_str] = []
            
        self.itinerary[date_str].append({
            "time": time,
            "activity": activity,
            "location": location
        })

    def view_itinerary(self):
        if not self.itinerary:
            print("No activities planned yet!")
            return

        print(f"\nVacation Itinerary for {self.destination}")
        print(f"Trip Duration: {self.start_date.date()} to {self.end_date.date()}\n")
        
        for date in sorted(self.itinerary.keys()):
            print(f"=== {date} ===")
            day_activities = sorted(self.itinerary[date], key=lambda x: x["time"])
            for activity in day_activities:
                print(f"{activity['time']} - {activity['activity']} at {activity['location']}")
            print()

def main():
    planner = VacationPlanner()
    
    while True:
        print("\n=== Vacation Planner ===")
        print("1. Set trip details")
        print("2. Add activity")
        print("3. View itinerary")
        print("4. Exit")
        
        choice = input("Enter your choice (1-4): ")
        
        if choice == "1":
            planner.set_trip_details()
        elif choice == "2":
            if not planner.destination:
                print("Please set trip details first!")
                continue
            planner.add_activity()
        elif choice == "3":
            planner.view_itinerary()
        elif choice == "4":
            print("Thank you for using Vacation Planner!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
