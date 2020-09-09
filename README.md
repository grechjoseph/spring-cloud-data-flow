<h1>Spring Cloud Data Flow</h1>
<h2>Deployment</h2>
<ol>
  <li>
    To deploy Spring Cloud Data Flow locally, run the following command: <b>docker-compose up -d</b>
  </li>
  
  <li>
    Once all Docker images' logs stop, test that the environment loads by navigating to <a href='http://localhost:9393'>http://localhost:9393/dashboard</a>.
  </li>
</ol>
<b>NOTE: </b> By default, the <b>Spring Cloud Data Flow</b> docker image has the directory of the docker-compose file mounted on the docker image at <b>/root/scdf/</b>.
<h2>Creating a Task</h2>
<ol>
  <li>
    Navigate to <a href='http://localhost:/9393/dashboard'>Dashboard</a> -> Tasks.
  </li>
  
  <li>
    Click <b>Create task(s)</b>.
  </li>
  
  <li>
    For the task definitions, type "timestamp" (a predefined application already available in the Spring Cloud Data Flow deployment).
  </li>
  
  <li>
    Click <b>Create task</b> and provide the task a name.
  </li>
  
  <li>
    Once at the Tasks list, click the ► button next to the task in order to deploy it.
  </li>
  
  <li>
  In the next screen, leave the default (empty) application properties, and click <b>Launch the task</b>.
  </li>
  
  <li>
  Hit the <b>Refresh</b> button until the task's status changes to <b>COMPLETE</b>.
  </li>
  
  <li>
  Click the task's name to go to its summary page.
  </li>
  
  <li>
  Switch to the <b>Executions</b> page and click the task's ID to see the logs of the task that was deployed under the <b>Logs</b> section.
  </li>
</ol>
<h2>Creating a Stream</h2>
A Stream is a flow of different tasks in the format of SOURCE -> TRANSFORMER/PROCESSOR -> SINK.
<ol>
  <li>Navigate to <a href='http://localhost:9393/dashboard'>Dashboard</a> -> Streams.</li>
  <li>Click on <b>Create Stream(s)</b>.</li>
  <li>For the stream definition, provide: <b>infile: file | outfile: file</b>, where <b>infile</b> and <b>outfile</b> are just labels for the two identical tasks.</li>
  <li>Click on <b>Create Stream(s)</b> and provide a name for the Stream.</li>
  <li>Click on the ► button to Deploy Stream.</li>
  <li>
    In the properties page, under <b>Applications Properties</b>, provide the following:
    <ul>
      <li>infile: direction = /root/scdf/in</li>
      <li>outfile: directory = /root/scdf/out</li>
    </ul>
    (Remember the NOTE above of the docker-compose file's directory being redirect as /root/scdf to the Dataflow Server image.)
  </li>
  <li>Click on <b>Deploy Stream</b>.</li>
  <li>Once the Stream status reads <b>DEPLOYED</b>, the two directory (<b>in</b> and <b>out</b>) should have been created next to the docker-compose file.</li>
  <li>Create a sample text file with some content and save it in the <b>in</b> folder.</li>
  <li>Navigate to the <b>out</b> folder, and you should find a file called <b>file-sink</b>.</li>
  <li>Open it using Notepad, and you should find that the content of this file is the same as the text file created in the <b>in</b> folder.<li>
</ol>

Essentially, the <b>infile</b> task picked up the file from the <b>in</b> folder (by polling the directory), published the contents to the <b>outfile</b>, which then saved its contents to the <b>/out/file-sink</b> file.
