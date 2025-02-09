# brick_booking.py

class BrickBooking:
    def __init__(self, total_bricks):
        self.total_bricks = total_bricks
        self.available_bricks = total_bricks
        self.booked_bricks = []

    def book_brick(self, name, quantity):
        if quantity <= 0:
            return "Quantity must be a positive number."
        
        if quantity > self.available_bricks:
            return f"Not enough bricks available. Only {self.available_bricks} bricks left."

        self.available_bricks -= quantity
        self.booked_bricks.append({"name": name, "quantity": quantity})
        return f"Booking confirmed for {quantity} brick(s). {self.available_bricks} bricks remaining."

    def cancel_booking(self, name, quantity):
        for booking in self.booked_bricks:
            if booking["name"] == name and booking["quantity"] >= quantity:
                booking["quantity"] -= quantity
                self.available_bricks += quantity
                if booking["quantity"] == 0:
                    self.booked_bricks.remove(booking)
                return f"Booking for {quantity} brick(s) canceled. {self.available_bricks} bricks available."
        
        return f"No booking found for {name} with {quantity} bricks to cancel."

    def check_availability(self):
        return f"{self.available_bricks} bricks available."

    def list_bookings(self):
        return self.booked_bricks


def main():
    total_bricks = 100
    brick_system = BrickBooking(total_bricks)

    print("Welcome to the Brick Booking System!")
    while True:
        print("\n1. Book a Brick")
        print("2. Cancel Booking")
        print("3. Check Availability")
        print("4. List Bookings")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            name = input("Enter your name: ")
            quantity = int(input("Enter the number of bricks to book: "))
            print(brick_system.book_brick(name, quantity))

        elif choice == '2':
            name = input("Enter your name: ")
            quantity = int(input("Enter the number of bricks to cancel: "))
            print(brick_system.cancel_booking(name, quantity))

        elif choice == '3':
            print(brick_system.check_availability())

        elif choice == '4':
            print("Current Bookings: ", brick_system.list_bookings())

        elif choice == '5':
            print("Exiting the Brick Booking System...")
            break
        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()
