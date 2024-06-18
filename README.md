# codsoft_taskno5
import tkinter as tk
from tkinter import messagebox, simpledialog
from tkinter.scrolledtext import ScrolledText
class ContactBook:
    def __init__(self, window):
        self.window = window
        self.window.title("Contact Book")
        self.contacts = []
        tk.Label(window, text="Name:").grid(row=0, column=0, sticky="e")
        self.name_entry = tk.Entry(window)
        self.name_entry.grid(row=0, column=1)
        tk.Label(window, text="Phone:").grid(row=1, column=0, sticky="e")
        self.phone_entry = tk.Entry(window)
        self.phone_entry.grid(row=1, column=1)
        tk.Label(window, text="Email:").grid(row=2, column=0, sticky="e")
        self.email_entry = tk.Entry(window)
        self.email_entry.grid(row=2, column=1)
        tk.Label(window, text="Address:").grid(row=3, column=0, sticky="e")
        self.address_entry = tk.Entry(window)
        self.address_entry.grid(row=3, column=1)
        tk.Button(window, text="Add Contact", command=self.add_contact).grid(row=4, column=0, columnspan=2, pady=10)
        tk.Button(window, text="View Contacts", command=self.view_contacts).grid(row=5, column=0, columnspan=2, pady=10)
        tk.Button(window, text="Search Contact", command=self.search_contact).grid(row=6, column=0, columnspan=2, pady=10)
        tk.Button(window, text="Update Contact", command=self.update_contact).grid(row=7, column=0, columnspan=2, pady=10)
        tk.Button(window, text="Delete Contact", command=self.delete_contact).grid(row=8, column=0, columnspan=2, pady=10)
    def add_contact(self):
        name = self.name_entry.get()
        phone = self.phone_entry.get()
        email = self.email_entry.get()
        address = self.address_entry.get()
        if name and phone:
            self.contacts.append({"Name": name, "Phone": phone, "Email": email, "Address": address})
            messagebox.showinfo("Success", "Contact added successfully!")
        else:
            messagebox.showerror("Error", "Name and phone number are required!")
    def view_contacts(self):
        if self.contacts:
            contact_list = "\n".join([f"{contact['Name']}: {contact['Phone']}" for contact in self.contacts])
            contact_view = tk.Toplevel(self.window)
            contact_view.title("Contacts")
            contact_view.geometry("400x300")
            text_area = ScrolledText(contact_view, width=40, height=20)
            text_area.insert(tk.END, contact_list)
            text_area.pack(expand=True, fill="both")
        else:
            messagebox.showinfo("Contacts", "No contacts found!")
    def search_contact(self):
        search_query = simpledialog.askstring("Search Contact", "Enter name or phone number to search:")
        if search_query:
            found_contacts = [contact for contact in self.contacts if search_query.lower() in contact['Name'].lower() or search_query in contact['Phone']]
            if found_contacts:
                result_text = "\n".join([f"{contact['Name']}: {contact['Phone']}" for contact in found_contacts])
                messagebox.showinfo("Search Results", result_text)
            else:
                messagebox.showinfo("Search Results", "No matching contacts found!")
        else:
            messagebox.showinfo("Search Results", "Search query cannot be empty!")
    def update_contact(self):
        pass
    def delete_contact(self):
        pass
if __name__ == "__main__":
    root = tk.Tk()
    app = ContactBook(root)
    root.mainloop()
