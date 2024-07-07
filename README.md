use std::io::{self, Write};

fn main() {
    loop {
        println!("Simple Rust Calculator");
        println!("Enter the first number:");
        let num1 = read_number();

        println!("Enter the operation (+, -, *, /):");
        let op = read_operation();

        println!("Enter the second number:");
        let num2 = read_number();

        let result = match op {
            '+' => num1 + num2,
            '-' => num1 - num2,
            '*' => num1 * num2,
            '/' => {
                if num2 == 0.0 {
                    println!("Error: Division by zero");
                    continue;
                }
                num1 / num2
            },
            _ => {
                println!("Invalid operation");
                continue;
            }
        };

        println!("Result: {}", result);

        println!("Do you want to perform another calculation? (y/n):");
        let mut again = String::new();
        io::stdin().read_line(&mut again).expect("Failed to read input");
        if again.trim().to_lowercase() != "y" {
            break;
        }
    }
}

fn read_number() -> f64 {
    loop {
        let mut input = String::new();
        io::stdin().read_line(&mut input).expect("Failed to read input");
        match input.trim().parse::<f64>() {
            Ok(num) => return num,
            Err(_) => println!("Invalid number, please try again:"),
        }
    }
}

fn read_operation() -> char {
    loop {
        let mut input = String::new();
        io::stdin().read_line(&mut input).expect("Failed to read input");
        let op = input.trim().chars().next().unwrap_or(' ');
        if "+-*/".contains(op) {
            return op;
        } else {
            println!("Invalid operation, please try again:");
        }
    }
}
