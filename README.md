import netmiko
import difflib
import difflib as dl

connection = {
    'device_type' : 'cisco_ios',
    'host' : '192.168.56.101',
    'username' : 'cisco', #[It's already setup on the router]
    'password' : 'cisco123!', #[It's already setup on the router]
    'secret' : 'class123!' #[It's already setup on the router]
}

print('MENU')
connection['username'] = input('Enter the Username of device: ')
connection['password'] = input('Enter the Password of device: ')
connection['secret'] = input('Enter the  of Secret Password of device: ')
choice = input('Type (1) for File Comparison & Type (2) for offline comparison: ')

if choice == '1':
    router = netmiko.ConnectHandler(**connection)
    router.enable()
    running_config = router.send_command('show running-config')
    startup_config = router.send_command('show startup-config')
    for diff in dl.context_diff(running_config.split('/n'), startup_config.split('/n')):
        print(diff)



if choice == '2':
    router = netmiko.ConnectHandler(**connection)
    router.enable()
    running_config = router.send_command('show running-config')
    choice1 = input('Do you want compare between running configuration and offline configuration? [Y] or [N]')
    file = open('config-local.txt', "r")
