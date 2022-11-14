import pexpect
import difflib
connection = {
    'device_type' : 'cisco_ios',
    'hostname' : '192.168.1.1',
    'user_name' : 'cisco', #[It's already setup on the router]
    'password' : 'cisco123!', #[It's already setup on the router]
    'secret' : 'class123!' #[It's already setup on the router]
}
print('MENU')
connection['user_name'] = input('Enter the Username of device')
connection['password'] = input('Enter the Password of device')
connections['secret'] = input('Enter the  of Secret Password of device')
choice = input('Type (1) for File Comparison & Type (2) for offline comparison')

if choice == '1':
    router = netmiko.ConnectionHandler(**connection)
    router.enable()
    running_config = router.send_command('show running-config')
    startup_config = router.send_command('show startup-config')



if choice == '2':
    router = netmiko.ConnectionHandler(**connection)
    router.enable()
    running_config = router.send_command('show running-config')
    choice1 = input('Do you want compare between running configuration and offline configuration? [Y] or [N]')
    file = open('configuration.txt', "r")
