<head>
<h1>Ansible Playground</h1>
</head>
<body>
This is a simple Ansible role to show off some basic features of Ansible in a graphical manner. It's a good way to see some basic linux filesystem tasks on your local machine. It's designed so that you can clone the repo and look at some Ansible while offline.
<br>
<h2>Steps to engage</h2>
<ol>
<li>Install Ansible on your linux machine (I used v2.2)</li>
<li>Navigate to the project's top level directory, you should see myplaybook.yml</li>
<li>Navigate to <i>roles/bpleines.playground/files/</i> and open index.html with your favorite web browser. There shouldn't be much here</li>
<li>Enter the command <i>ansible-playbook myplaybook.yml -vvv --step</i> to begin execution of the playbook</li>
</ol>
<h3>Stepping through the playbook run</h3>
The playbook tasks run sequetially. After each task that you enter yes to step through, it is useful to look at the yml code that created it.
<ul>
<li> You should notice that your name and profession are not listed properly. Hit ctrlC to exit the playbook run, as we need to update these. </li>
<li>Open myplaybook.yml in a text editor, you should see that my_name and my_profession are commented out. Uncomment them and add your name and profession. </li>
<li> Run the command <i>ansible-playbook myplaybook.yml -vvv --step again</i>. You just changed the variables from their role default values; their changes are reflected in your new run.</li>
<li> After you execute the step titled "Remove the default body content" refresh your browser. You should have a snazzy Red Hat background. </li>
<li> Notice that the following "Overwrite..." task was skipped - this is due to a conditional on the task.
</ul>
<h3> Executing the revert </h3> 
<ul>
<li>Open myplaybook.yml and uncomment the revert: true variable declarance. </li>
<li>Run <i>ansible-playbook myplaybook.yml -vvv</i>. You won't be prompted for a step by step, but notice that most of the previously executed tasks are skipped, but the "Overwrite..." task is executed. </li>
<li> Refresh your web browser. You're back to square one.</li>
</ul>

<h3> Next steps </h3>
Take a look at the <i>main.yml, apply.yml, and revert.yml</i> tasks. If it isn't clear what a keyword does, the Ansible documents will help highlight this. The tasks are kept very simple so that you can change and play with them. Ansible is intended for configuring/maintaining states much more complex than this, and ansible-playground deals with a very small subset of the Ansible modules available.

It's also important to note that the ansible-playground role breaks a major design paradigm (idempotentcy) to simplify its design. Ideally, you should be able to run <i>apply.yml</i> against a host as many times as you want because Ansible modules monitor the state of a machine. Because we are making local changes to files, running <i> apply.yml </i> several times in a row will have unintended consequences. Luckily, even if you've done this, running the revert will return the file to it's original state.
</body>


