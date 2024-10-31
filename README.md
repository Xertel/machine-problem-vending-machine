# machine-problem-vending-machine
 An application with interface for computing change value from the inputted owed and money values

# Vending Machine Application

This project is a Vue 3 application that simulates a vending machine interface. The vending machine takes in items selected from a shop interface, calculates the total owed amount, accepts an inserted bill in Philippine currency, and displays the change to the user.

## Features

- **Shop Interface**: Users can browse and select items, each with a specific price.
- **Item Cards**: There's an option to accumulate owed value from clicking "Buy" from the item cards within the shop interface.
- **Total Owed**: User can input value directly and/or accumulate value from the shop interface. The total owed amount is calculated in real-time.
- **Bill Input and Change Display**: Users can input a bill, and the application calculates the user's change based on the total owed amount.
- **Philippine Currency Support**: Handles input and displays change in Philippine Pesos (PHP) denominations.

## Prerequisites

Ensure that you have **Node.js** and **npm** installed. You can download them from [nodejs.org](https://nodejs.org/).

If you don’t have Vue CLI installed globally, install it using:

```bash
npm install -g @vue/cli
```

## Project Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Xertel/machine-problem-vending-machine.git
   cd machine-problem-vending-machine
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Run the development server**:
   ```bash
   npm run dev
   ```
   This command starts a development server, usually accessible at [http://localhost:5173](http://localhost:5173) (or the URL shown in your terminal).

## Components

### `ShopInterface.vue`

- Displays available items for sale, each with a name and price.
- Manages prices of items available.
- Allows users to add items' costs to the total owed value.
- Emits an event to the parent component to update the total owed value.

### `ItemCard.vue`

- Displays an item in the shop that has a corresponding cost value.
- An item can be chosen for its cost to be added to the total owed value.

### `PaymentInterface.vue`

- Displays and accepts total owed value.
- Accepts input bill from dropdown of possible denominations.
- Calculates the change based on the total owed amount after clicking "Get Change" button.
- Displays the change in Philippine currency denominations (PHP bills and coins).
- Displays a corresponding error message when an input is invalid.

### `VendingMachine.vue` (Main Component)

- Parent component that houses `ShopInterface` and `PaymentInterface`.
- Manages the main data flow, including item prices, the total owed, and the user's inserted bill.

## Data Flow

1. **ShopInterface Component**: User selects items → emits selected item to `VendingMachine.vue`.
2. **VendingMachine.vue**: Receives item costs and updates `totalOwed` → passes `totalOwed` to `PaymentInterface.vue`.
3. **Payment Component**: Can accept direct user input for owed value, accepts user bill input, calculates change → displays change in certain denominations.

## Usage

1. (Optional) Select items to "buy" from the **Shop Interface**.
2. Review or change directly the owed value in the **Payment Interface**.
3. Select an input bill to be paid in the **Payment Interface** section.
4. Click "Get Change" button to view the change and denominations if any change is due.
5. Upon clicking the "Get Change" button, if there is an invalid input, a corresponding error message will be shown.

## Output and Error Handling

1. The valid input range for owed value is 0 < owed <= 1000.
2. The output of "Get Change" button will be shown in the end section of **Payment Interface**.
3. If the owed value exceeds the largest possible input bill (1000), output "You owe too much".
4. If the owed value exceeds the inputted bill, output "Please put more money." 
5. If the owed value is a negative value, output "Invalid input!".
6. If change is computed and the owed value equals to input bill, output "There is no more change. Thanks for shopping!".
7. If the change is shown successfully, output "Thanks for shopping!".

## Currency Support

This application supports Philippine currency, displaying change in bills and coins (PHP 1000, 500, 200, 100, 50, 20, 10, 5, and 1).
