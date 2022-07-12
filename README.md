<div class="scrollable-container" ng-transclude=""> <div markdown="fileTab.file.challenge.instructions" multi-language="true" class="markdown collapsed"><h1>Node and Express: Assessment</h1><p>This lesson should take you between 60 and 90 minutes. If you spend longer than that on this lesson, reach out for help!</p>
<h2>Instructions</h2><p>Your goal for this lesson is to get the tests to pass. To do so, you will be creating a simple server with three distinct routes and error handling. Your server should follow the structure you've learned in the course. Complete the following tasks to pass the tests and this assessment.</p>
<p><em><strong>Note:</strong> Because the <code>app.js</code> file is currently empty, your tests will fail immediately. These failures will revert back to normal test failures once you have the basic app structure up and running.</em></p>
<h3>Existing files</h3><table>
<thead>
<tr>
<th>File path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>app.js</code></td>
<td>An empty file. Place your application code here.</td>
</tr>
<tr>
<td><code>server.js</code></td>
<td>An empty file. Place your server code here.</td>
</tr>
<tr>
<td><code>middleware/validateZip.js</code></td>
<td>Includes a function definition. You will need to complete this middleware function.</td>
</tr>
<tr>
<td><code>utils/getZoos.js</code></td>
<td>A function that retrieves zoos based off of a zip. You will need to use this function, but you should not need to modify it.</td>
</tr>
<tr>
<td><code>test/assignment.test.js</code></td>
<td>The tests your code will run against. You do not need to edit this file.</td>
</tr>
</tbody>
</table>
<h3>Tasks</h3><ol>
<li><p>In the <code>app.js</code> file, require Express, create an Express application, and export that application.</p>
</li>
<li><p>In the <code>server.js</code> file, require the exported Express application from the <code>app.js</code> file and start your server.</p>
</li>
<li><p>(<em><strong>Note:</strong> Skip this step for now.</em>) Use the <code>morgan</code> middleware. Make sure that it is included above any routes.</p>
</li>
<li><p>In the <code>app.js</code> file, you will create three routes. See below for more information on the routes.</p>
</li>
<li><p>In the <code>middleware/validateZip.js</code> file, you will fill in the function definition to create middleware that is checking for a valid zip code. Read the instructions below as you will <em>not</em> be building a robust zip code validator.</p>
</li>
<li><p>In the <code>app.js</code> file, you will create error handlers in the case of a missing route and a general error handler.</p>
</li>
</ol>
<p><em><strong>Note:</strong> If you are having trouble getting your tests to pass but think you've gotten it right, make sure to check for punctuation and spelling. The tests are looking for exact string matches.</em></p>
<h3>Routes</h3><p>To complete this project, you will create the following routes:</p>
<h4><code>/check/:zip</code></h4><p>This route will respond with a short message saying whether or not the provided zip code is recorded in the <code>getZoos.js</code> file. Use the <code>getZoos()</code> function and pass in the zip code provided via the route parameter to receive the zoos in that zip code.</p>
<ul>
<li><p>If the zip is a valid zip code (see middleware below) and matches an existing zip code, respond with a short message.</p>
</li>
<li><p>If the zip is a valid zip code (see middleware below) and <em>does not</em> match an existing zip code, respond with a different short message.</p>
</li>
</ul>
<p><strong>Example request URL</strong></p>
<pre><code>http://localhost:5000/check/07502
</code></pre><p><strong>Matching zip response</strong></p>
<pre><code>07502 exists in our records.
</code></pre><p><strong>No matching zip response</strong></p>
<pre><code>12345 does not exist in our records.
</code></pre><h4><code>/zoos/:zip</code></h4><p>This route will respond with zoos for the specified zip code. Use the <code>getZoos()</code> function and pass in the zip code provided via the route parameter to receive the zoos for that zip.</p>
<ul>
<li><p>If the zip is a valid zip code (see middleware below) and matches an existing zip code, respond with a short message and the zoos <em>joined by a semicolon.</em></p>
</li>
<li><p>If the zip is a valid zip code (see middleware below) and <em>does not</em> match an existing zip code, respond with a short message.</p>
</li>
</ul>
<p><strong>Example request URL</strong></p>
<pre><code>http://localhost:5000/zoos/07502
</code></pre><p><strong>Correct response with single zoo</strong></p>
<pre><code>02121 zoos: COMMONWEALTH ZOOLOGICAL CORPORATION, Boston, Massachusetts
</code></pre><p><strong>Correct response with multiple zoos</strong></p>
<pre><code>33890 zoos: HARDEE COUNTY BOARD OF COUNTY COMMISSION, Zolfo Springs, Florida; PEACE RIVER REFUGE &amp; RANCH INC, Zolfo Springs, Florida
</code></pre><p><strong>Correct response with no zoos</strong></p>
<pre><code>07502 has no zoos.
</code></pre><h4><code>/zoos/all</code></h4><p>This route will respond with all zoos, but will only do so if the <code>admin</code> query parameter is provided and the value is set to <code>true</code>. Use the <code>getZoos()</code> function and pass in <em>no arguments</em> to receive all zoos.</p>
<ul>
<li><p>If these constraints <em>are</em> met, the route will respond with a brief message followed by all of the zoos <em>joined by a semicolon.</em></p>
</li>
<li><p>If these constraints <em>aren't</em> met, the route will respond with an error message.</p>
</li>
</ul>
<p><strong>Correct request URL</strong></p>
<pre><code>http://localhost:5000/zoos/all?admin=true
</code></pre><p><strong>Correct query parameter response</strong></p>
<pre><code>All zoos: WILDLIFE CONSERVATION SOCIETY, Bronx, New York; HARDEE COUNTY BOARD OF COUNTY COMMISSION, Zolfo Springs, Florida; PEACE RIVER REFUGE &amp; RANCH INC, Zolfo Springs, Florida; CLOSE UP CREATURES L L C, Naples, Florida; KOWIACHOBEE ANIMAL PRESERVE INC, Naples, Florida; PRIVATE OWNER, Naples, Florida; COMMONWEALTH ZOOLOGICAL CORPORATION, Boston, Massachusetts
</code></pre><p><strong>Incorrect query parameter response</strong></p>
<pre><code>You do not have access to that route.
</code></pre><h3>Middleware</h3><p>Update the <code>validateZip()</code> function so that it validates an incoming parameter called <code>zip</code> according to the following constraints. You do not need to do any more validation than this to get the tests to pass.</p>
<ol>
<li><p>The zip code must be five characters long.</p>
</li>
<li><p>The zip code must be all numeric. That is, no non-digit characters are allowed.</p>
</li>
</ol>
<p>Based on whether or not the zip code is valid, your server should respond in the following way:</p>
<ul>
<li><p>If the zip code <em>is</em> valid, move along to the next middleware function.</p>
</li>
<li><p>If the zip code <em>is not</em> valid, move along to the <em>error handler function.</em></p>
</li>
</ul>
<p><strong>Invalid zip code response</strong></p>
<pre><code>Zip (ABCDE) is invalid!
</code></pre><h3>Error handling</h3><p>If the user goes to a route that is not defined, respond with the following message:</p>
<div class="language-tabset"><div class="language-tab language-md"><pre><code class="lang-md">That route could not be found!
</code></pre>
</div></div></div> <score-card-instructions challenge="fileTab.file.challenge"><!----></score-card-instructions> </div>