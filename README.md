Clarity create_resource Moodle web service
------------------------------------------

Installation
-------------

1- Put the clarity folder in /local/

2- Edit local/clarity/version.php and increase the plugin version.
   

   This should trigger a Moodle upgrade and the new web service should be available in the site administration
   (Site administration -> Notifications)
   
3- You will need to assign Moodle permissions and access as suits your Moodle installation.


Call Web Service
-----------------

To call the create_resource web service, send a REST POST request to the Moodle web service api.

    http://YOUR_MOODLE_SITE_URL/webservice/rest/server.php?wstoken=YOUR_WEB_SERVICE_TOKEN&wsfunction=local_clarity_create_resource&moodlewsrestformat=json
	
The parameters that can be passed are;

    {
        'courseid':  The course id,
        'sectionid':  The section id,
        'type':  file, label, or folder
        'displayname':  The name of the resource in Moodle,
        'mainfile':  The main file. To be used with type folder, this is the file in the folder that will be opened when the a user clicks on the resource in Moodle
        'mainfilepath':  The path to the main file from the root of the folder. Must start and end with /,
        'labeltext':  The label content,
        'labeltextformat':  The label content format. markdown or html,
    }


The web service can create two resource types, file or label.

Files should be sent as Multipart-Encoded File.

Label content is passed through the labeltext attribute

A zipped folder can be sent identified with a type of 'folder'. The folder will still be a file resource but the
folder will be unzipped and can be navigated in Moodle.

If a mainfile attribute is specified, that file within the folder will be opened when a user clicks on the resource in Moodle.
This can be useful for sending HTML pages that have bundled resources.