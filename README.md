<h1>File Permissions in Linux</h1>

<h2>Description</h2>
<p>
This project was part of a system hardening initiative focused on securing data access within a Linux environment. The task involved auditing and correcting file and directory permissions inside a research team’s <code>projects</code> directory. The goal was to align access rights with security policy—ensuring only authorized users could read, write, or execute files—while eliminating permission risks that could lead to data exposure or modification.
</p>

<h2>Languages and Utilities Used</h2>
<ul>
  <li><b>Bash (Linux Shell)</b></li>
  <li><b>chmod</b></li>
  <li><b>ls -la</b></li>
</ul>

<h2>Environments Used</h2>
<ul>
  <li><b>Ubuntu 22.04 LTS</b></li>
  <li><b>Terminal (Bash)</b></li>
  <li><b>Linux Filesystem</b></li>
</ul>

<h2>Program Walk-Through</h2>

<p><b>Step 1: Audit file and directory permissions</b></p>
<p>To begin, I used the following command to list all files in the <code>projects</code> directory, including hidden ones:</p>

<pre><code>ls -la</code></pre>

<p align="center"> <br/>
<img src="https://i.imgur.com/KFEW8na.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
  
<p>
This command provided a complete view of each file's permission string. The output showed five project files, a hidden file <code>.project_x.txt</code>, and a subdirectory <code>drafts</code>. Each entry included a 10-character string indicating type and access rights for user, group, and others.
</p>

<p><b>Step 2: Interpret permission strings</b></p>
<ul>
  <li>Character 1 – File type (<code>-</code> for regular file, <code>d</code> for directory)</li>
  <li>Characters 2–4 – User permissions (e.g., <code>rw-</code>)</li>
  <li>Characters 5–7 – Group permissions</li>
  <li>Characters 8–10 – Other (world) permissions</li>
</ul>
<p>
For example, <code>-rw-rw-r--</code> means the file is a regular file; the user and group can read/write, while others can only read.
</p>

<p><b>Step 3: Remove write access from "others" on <code>project_k.txt</code></b></p>
The organization determined that others shouldn't have write access to any of their files. To comply with this, I referred to the file permissions that I previously returned. I determined project_k.txt must have the write access removed for other.
<p>This file incorrectly allowed write access for all users. To remove that, I executed:</p>

<pre><code>chmod o-w project_k.txt</code></pre>

<p>
The updated permissions were confirmed using <code>ls -la</code>, which showed that write access was successfully removed from the "others" category.
</p>

<p align="center">
<img src="https://i.imgur.com/12HxstZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p><b>Step 4:Change file permissions on a hidden file (hidden archived file)</b></p>
<p>The research team at my organization recently archived project_x.txt. They do not want anyone to have write access to this project, but the user and group should have read access.
   
</p>

<p align="center">
The following code demonstrates how I used Linux commands to change the permissions:<br/>
<img src="https://i.imgur.com/9vu5w2K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p> The first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. I know <code>.project_x.txt</code> is a hidden file because it starts with a period (<code>.</code>). In this example, I removed write permissions from the user and group, and added read permissions to the group. I removed write permissions from the user with <code>u-w</code>. Then, I removed write permissions from the group with <code>g-w</code>, and added read permissions to the group with <code>g+r</code>. 
</p>

<p>
These commands ensured that neither the user nor the group could modify the file, but it remained visible and readable to the necessary team members.
</p>

<p><b>Step 5: Restrict access to the <code>drafts</code> directory</b></p>
<p>
My organization only wants the researcher2 user to have access to the drafts directory and its contents. This means that no one other than researcher2 should have execute permissions. To enforce that only <code>researcher2</code> could traverse the <code>drafts</code> directory, I removed group-level execute permissions.
</p>


<p align="center">
 The following code demonstrates how I used Linux commands to change the permissions:
<br/>
<img src="https://i.imgur.com/GitTtQG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p>
The output here displays the permission listing for several files and directories. Line 1 indicates the current directory (projects), and line 2 indicates the parent directory (home). Line 3 indicates a regular file titled <code>.project_x.txt</code>. Line 4 is the directory (drafts) with restricted permissions. Here you can see that only <code>researcher2</code> has execute permissions.  It was previously determined that the group had execute permissions, so I used the <code>chmod</code> command to remove them. The <code>researcher2</code> user already had execute permissions, so they did not need to be added.
</p>

<h2>Summary</h2>
<p>
This project demonstrates the use of Linux permissions commands to support secure, policy-compliant file management. By auditing and correcting permissions with <code>ls -la</code> and <code>chmod</code>, I enforced tighter access controls and reduced the risk of unauthorized activity in the system. All changes were verified in real time and reflected the organization's access standards.
</p>
