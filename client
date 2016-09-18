import xmlrpc.client

proxy = xmlrpc.client.ServerProxy('http://192.168.1.9:8000')

loop = True
valid_commands = ['add', 'remove', 'modify', 'exit', 'view']
USER_PROMPT = 'To add a student, enter "Add"; to remove a student,' \
            ' enter "Remove"; to modify a student, enter "Modify"; to view' \
            ' the student list, enter "View" to exit, enter "Exit" \n'
            
print('Welcome to the class registration system \n')

while loop == True:

    user_command = input(USER_PROMPT)

    if user_command.strip().lower() not in valid_commands:
        print('That command is not valid')        
        loop == True

    elif user_command.strip().lower() == 'exit':
        loop = False

    elif user_command.strip().lower() == 'add':
        name = input('Please enter student name in "last, first" format: ')
        address = input('Please enter student address: ')
        phone = input('Please enter student phone #: ')
        proxy.add(name, address, phone)

    elif user_command.strip().lower() == 'remove':
        del_id = input('Please enter student ID of student to be deleted: ')        
        proxy.remove(del_id)

    elif user_command.strip().lower() == 'modify':
        mod_id = input('Please enter student ID of student to be modified: ')
        mod_record = proxy.view(mod_id)        
        print('Student ID {} is: \n'
            'Name: {}, Address: {}, Phone: {}'.format(
            mod_id, 
            mod_record['name'], 
            mod_record['address'], 
            mod_record['phone']
            ))
        mod_field = input(
            'Would you like to modify the name ("N"), address ("A"),'
            'or phone # ("P")? ').strip().lower()
        if mod_field == 'n':
            mod_new = input('Please enter new name: ')
        elif mod_field == 'a':
            mod_new = input('Please enter new address: ')
        elif mod_field == 'p':
            mod_new = str(input('Please enter new phone #: '))
        else:
            print('That command not recognized')
        proxy.modify(mod_id, mod_field, mod_new)

    elif user_command.strip().lower() == 'view':
        student_dict = proxy.acquire_dict()
        for key in student_dict:
            print('ID: {}; Name: {}; Address: {}; Phone: {}'.format(
            key, student_dict[key]['name'], student_dict[key]['address'],
            student_dict[key]['phone']))
        print('\n')
    
    else:
        loop = False
