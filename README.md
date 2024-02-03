# 2024_02_02_HelloCarRcFromScratch
We try to learn how we can use Scratch as an controller for third application like Hello Car RC


- https://youtu.be/CrI-iCATU2g
- https://scratch.mit.edu/cloudmonitor/960534356/
- https://scratch.mit.edu/projects/960534356/
- https://en.scratch-wiki.info/wiki/Cloud_Data

``` python



from scratchclient import ScratchSession

def read_file(file_path):
    try:
        with open(file_path, 'r') as file:
            file_content = file.read()
            return file_content
    except FileNotFoundError:
        return f"Error: File '{file_path}' not found."
    except Exception as e:
        return f"Error: {e}"


password= read_file("password.txt")
name ="EloiStree"

session = ScratchSession(name, password)


# lots of other stuff

print(session.get_studio(34580905).description)
print(session.get_project(960534356).get_comments()[0].content)

print("T0")

connection = session.create_cloud_connection(960534356)


print("T1")

@connection.on("set")
def on_set(variable):
    print(variable.name, variable.value)
    

print("T2")
connection.set_cloud_variable("Test", 42)
print(connection.get_cloud_variable("Test"))

print("End")

```
