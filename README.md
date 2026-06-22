import tkinter as tk

records = []

def add_record():
    selected_services = []

    if oil_var.get() == 1:
        selected_services.append(["Oil Change", 3000])
    if wash_var.get() == 1:
        selected_services.append(["Car Wash", 1000])
    if brake_var.get() == 1:
        selected_services.append(["Brake Service", 2500])
    if tire_var.get() == 1:
        selected_services.append(["Tire Rotation", 1500])

    records.append([
        customer_entry.get(),
        make_entry.get(),
        model_entry.get(),
        variant_entry.get(),
        selected_services
    ])

    customer_entry.delete(0, tk.END)
    make_entry.delete(0, tk.END)
    model_entry.delete(0, tk.END)
    variant_entry.delete(0, tk.END)

    oil_var.set(0)
    wash_var.set(0)
    brake_var.set(0)
    tire_var.set(0)

def show_records():
    output.delete("1.0", tk.END)

    for record in records:
        output.insert(tk.END, "Customer: " + record[0] + "\n")
        output.insert(tk.END, "Vehicle: " + record[1] + " " + record[2] + " " + record[3] + "\n")
        output.insert(tk.END, "Services:\n")

        for service in record[4]:
            output.insert(tk.END, service[0] + " - Rs. " + str(service[1]) + "\n")

        output.insert(tk.END, "-------------------------\n")

def generate_bill():
    output.delete("1.0", tk.END)

    if len(records) == 0:
        output.insert(tk.END, "No record found")
        return

    record = records[-1]
    total = 0

    output.insert(tk.END, "VEHICLE SERVICE BILL\n")
    output.insert(tk.END, "-------------------------\n")
    output.insert(tk.END, "Customer: " + record[0] + "\n")
    output.insert(tk.END, "Vehicle: " + record[1] + " " + record[2] + " " + record[3] + "\n\n")
    output.insert(tk.END, "Services:\n")

    for service in record[4]:
        output.insert(tk.END, service[0] + " - Rs. " + str(service[1]) + "\n")
        total += service[1]

    output.insert(tk.END, "\nTotal Bill: Rs. " + str(total))


root = tk.Tk()
root.title("Vehicle Service Management System")
root.geometry("500x600")

# Garage Title
tk.Label(root, text="S/J GARAGE", font=("Arial", 20, "bold")).pack(pady=10)

tk.Label(root, text="Customer Name").pack()
customer_entry = tk.Entry(root)
customer_entry.pack()

tk.Label(root, text="Vehicle Make").pack()
make_entry = tk.Entry(root)
make_entry.pack()

tk.Label(root, text="Vehicle Model").pack()
model_entry = tk.Entry(root)
model_entry.pack()

tk.Label(root, text="Vehicle Variant").pack()
variant_entry = tk.Entry(root)
variant_entry.pack()

tk.Label(root, text="Select Services").pack()

oil_var = tk.IntVar()
wash_var = tk.IntVar()
brake_var = tk.IntVar()
tire_var = tk.IntVar()

tk.Checkbutton(root, text="Oil Change (Rs.3000)", variable=oil_var).pack()
tk.Checkbutton(root, text="Car Wash (Rs.1000)", variable=wash_var).pack()
tk.Checkbutton(root, text="Brake Service (Rs.2500)", variable=brake_var).pack()
tk.Checkbutton(root, text="Tire Rotation (Rs.1500)", variable=tire_var).pack()

tk.Button(root, text="Add Customer Record", command=add_record).pack(pady=5)
tk.Button(root, text="Generate Bill", command=generate_bill).pack()
tk.Button(root, text="Show Records", command=show_records).pack()

output = tk.Text(root, height=18, width=55)
output.pack(pady=10)

root.mainloop()
