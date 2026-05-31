# What is Active Directory (AD)?
Definition
Active Directory (AD) is a directory service developed by Microsoft that stores and manages information about users, computers, groups, printers, and other resources in a network.

It provides:
	• Centralized Authentication 
	• Centralized Authorization 
	• Centralized Management

Think of AD as:
	The central identity database of an organization.

Why do SOC Analysts care so much about it?
Because if a hacker sneaks past the front door, their ultimate goal is to break into that Central Security Desk (Active Directory). If the hacker takes over AD, they can create a fake ID badge that lets them into every single room, server, and file in the entire company.


# Active Directory Core Components

1. Domain
A Domain is a logical collection of users, computers, groups, and resources managed by Active Directory.
Example
Company ABC has:

Employees
Laptops
Servers
Printers
All are managed under:

abc.local
This becomes the AD Domain.

2. Domain Controller (DC)
A Domain Controller (DC) is a server that runs Active Directory Domain Services (AD DS) and authenticates users within a domain.

