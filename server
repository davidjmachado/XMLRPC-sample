import xmlrpc

from xmlrpc.server import SimpleXMLRPCServer
from xmlrpc.server import SimpleXMLRPCRequestHandler

port_number = 8000

#Restrict to a particular path
class RequestHandler(SimpleXMLRPCRequestHandler):
    rpc_paths = ('/RPC2',)

#Create server.
server = SimpleXMLRPCServer((‘localhost’, port_number), 
                            requestHandler=RequestHandler, allow_none=True)
server.register_introspection_functions()

id_incrementer = [0]
students = dict()
valid_commands = ['add', 'remove', 'modify', 'exit', 'view']

print('Listening on port {}'.format(port_number))

#Register functions under different name.
def add_student(name, address, phone):
    student_id = id_incrementer[0]
    student_id += 1
    id_incrementer[0] = student_id
    students[str(student_id)] = dict(name=name, address=address, phone=phone)
    print('Added {}'.format(name))
    return

def remove_student(del_id):
    del students[del_id]
    print('Deleted Student ID #{}'.format(del_id))
    return
    
def modify_student(mod_id, mod_field, mod_new):
    if mod_field == 'n':
        field = 'name'        
        students[mod_id]['name'] = mod_new
    elif mod_field.strip().lower() == 'a':
        field = 'address'
        students[mod_id]['address'] = mod_new
    elif mod_field.strip().lower() == 'p':
        field = 'phone'
        students[mod_id]['phone'] = mod_new
    print('The {} field of Student ID #{} has been modified'.format(
        field, mod_id))
        
def display_students():
    student_dict = students   
    print('Displaying students in class registry')    
    return student_dict
    
def view_id(mod_id):
    mod_record = students[mod_id]
    print('Sent student ID #{} for modification'.format(mod_id))
    return mod_record
                
server.register_function(add_student, 'add')
server.register_function(remove_student, 'remove')
server.register_function(modify_student, 'modify')
server.register_function(display_students, 'acquire_dict')
server.register_function(view_id, 'view')

# Run the server's main loop
server.serve_forever()
