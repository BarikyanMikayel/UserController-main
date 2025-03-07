The first thing i did was to navigate into the webapp directory and run the npm install command to install any packages that might
be missing such as the angular packages (I do this with my react or next.js apps as well). I had to then rename the header.component.spec.ts
import to AppComponentsHeaderComponent and all of its references in the script. I did the same to application.component.spec.ts,
userdetails.component.spec.ts, Userslist.component.spec.ts, home.component.spec.ts. I then had to run dotnet restore
in order to restore the project.asset.json file. 

The first thing I noticed when I ran the application is that there where errors namely with the UserDBServices. What I did is I then 
navigated to the class UserDBServices nad looked into the IUserDBServices Interface. The first thing I noticed is that the 
Task<ServiceModel> UserLogin(bool UserName); Task had 2 references but when I looked into those specific references there were
errors namely dataType errors i.e, the Task was expecting a bool but instead a String was being passed. What I did was I simply
changed the bool to String and It solved the problem. The same went for the GetAllUsers Task where I had to insert the 
SelectionFilterModel from the InternalModels.cs as a parameter to get it to work. Lastly I noticed that DeleteSingleUser Task 
was giving issues as well and it was easy to fix as well what I did was I just added a string User parameter to it and it 
solved the problem. 

When I was done with that simple debugging I then ran the program to see if it ran successfully... I got an error that stated 
Exception Unhandled could not find file certs\paytequtils.pfx. It took me some time but i did figure out that obviously 
I would need to do something to produce a .pfx file and since I had both a .crt and a .key file in the certs folder I could 
run the following to get a .pfx file  I had to first change my directory to the certs directory and run the following command in 
the developer powershell -> | openssl pkcs12 -export -out paytequtils.pfx -inkey paytequtils.key -in paytequtils.crt | This 
command basically converted my .key and .crt files into an output .pfx file. After that I had my paytequtils.pfx file in my certs 
directory so I thought that I could run the program and see if there were any further errors... There were no errors i.e, the program 
ran successfully but now the problem was that it did not show anything in the following URL -> https://uc.paytequtils.com:5116/
So i thought to myself let me create a localhost instance to run the program and use a wwwroot/index.html to test and see if anything
shows up. 
