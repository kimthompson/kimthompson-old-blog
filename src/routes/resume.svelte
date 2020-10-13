<style>
h1, h2 {
  margin: 0;
}

h1 {
  margin-right: 1em;
}

h3 {
  color: var(--main-theme-color);
}

header {
  display: flex;
  color: var(--main-text-color);
  width: 100%;
  padding: 15px;
  justify-content: space-between;
}

header h2 {
  color: var(--main-theme-color);
}

header a {
  text-decoration: none;
  transition: .3s;
  padding: 0 5px;
}

header a:hover {
  color: var(--main-theme-color);
}

.contact {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: center;
  min-width: 370px;
}

.body {
  display: flex;
  align-items: flex-start;
  padding: 15px;
}

.main {
  padding-right: 15px;
}

.company {
  opacity: .3;
  font-size: .9em;
}

.job p {
  font-size: 1.1em;
}

.job ul {
  font-size: 1.1em;
}

.job ul li {
  margin: 0;
  padding: 0;
}

.job h5 {
  font-size: 1.1em;
  opacity: .3;
}

.job h6 {
  font-size: 1em;
  margin: 0;
}

.education h5 {
  font-size: 1.1em;
  margin: 0;
}

.education p {
  margin: 0;
}

.gpa {
  font-size: 1em;
  opacity: .3;
  padding-top: 5px;
}

.sidebar {
  text-align: right;
  min-width: 370px;
}

@media(max-width: 1200px) {
  .body {
    flex-direction: column;
  }

  .sidebar {
    text-align: left;
  }

  header {
    flex-direction: column;
  }

  .contact {
    text-align: left;
    align-items: flex-start;
  }
}
</style>

<svelte:head>
  <title>Resume - Kim Thompson</title>
</svelte:head>

<div>
  <header>
    <div>
      <h1>Kim Thompson</h1>
      <h2>Software Developer</h2>
      <p>Software developer with over 5 years of experience creating applications for web, mobile and Windows. A jack-of-all-trades who is passionate about pushing the web forward and making it better for everyone.</p>
    </div>
    <div class="contact">
      <span>135 Battle Creek Place, Saint Paul, MN 55119</span>
      <a href="+1-952-215-7255">
        952-215-7255
      </a>
      <a href="mailto:kimthompson@hey.com">
        kimthompson@hey.com
      </a>
      <a href="https://kimthompson.me">
        kimthompson.me
      </a>
      <a href="https://github.com/kimthompson">
        github.com/kimthompson
      </a>
      <a href="https://linkedin.com/in/kimberlyannthompson">
        linkedin.com/in/kimberlyannthompson
      </a>
    </div>
  </header>
  <div class="body">
    <section class="main">
      <h3>Experience</h3>
      <div class="job">
        <h4>Web Developer <span class="company">/ Minnesota Public Radio, Saint Paul, MN</span></h4>
        <h5>August 2018 - Present</h5>
        <p>Maintained American Public Media's old web applications and built new ones, using everything from server side Node and Rails to front end React and SCSS. Built large swaths of our reusable React component libraries and pushed for them to be open source and published on NPM. Vetted new tools like Next.js and React Native and architected initial solutions with them.</p>
        <h6 class="key">Key Accomplishments</h6>
        <ul>
          <li>Reworked APM Reports to pass all of Google's AMP rules so they would more frequently be the top result for the stories they broke. The day Curtis Flowers' conviction was overturned APM Reports had a record 175K pageviews.</li>
          <li>Proposed we move to Next.js when we had difficulty getting React and SSR to play nicely. Created a demo that convinced my boss and team that this would be more stable in the long run. Now all of our new development uses Next.js.</li>
          <li>Leveraged my journalism/dataviz background to work with the newsroom to revamp our election site. Created new maps and charts for the 2018 and 2020 elections.</li>
        </ul>
      </div>
      <div class="job">
        <h4>Associate Software Developer <span class="company">/ Design Center Inc., Saint Paul, MN</span></h4>
        <h5>February 2017 - August 2018</h5>
        <p>Developed applications for iOS, web and Windows. Some of these were large agile projects with a team of developers while others were small solo projects. Managed client and project manager expectations, sometimes helping them find solutions they did not think to ask for.</p>
        <h6 class="key">Key Accomplishments</h6>
        <ul>
          <li>Wrote the company's front end web standards. Attempted to teach the designers how to write solid HTML and CSS markup, as well as how to use VS Code. Stressed to the owner that markup and Javascript development is true software development that cannot be offloaded onto designers.</li>
        </ul>
      </div>
      <div class="job">
        <h4>Technology LDP Trainee <span class="company">/ Ameriprise Financial, Saint Paul, MN</span></h4>
        <h6>July 2015 - February 2017</h6>
        <p>Rotated between three different position over the course of 18 months as part of a program for recent graduates.</p>
        <h6 class="key">Key Accomplishments</h6>
        <ul>
          <li>Redesigned and wrote the front end for Ameriprise's advisor compensation application homepage, working within the limits of an old JSP, IE-only application.</li>
          <li>Tested and polished a client-facing dashboard built with Backbone.js.</li>
          <li>Conducted working sessions to complete disaster recovery plans for all of my department's applications.</li>
        </ul>
      </div>
      <div class="job">
        <h4>Product Strategy / Design Intern <span class="company">/ Pearson VUE, Bloomington, MN</span></h4>
        <h6>May 2014 - Aug 2014</h6>
        <p>Researched ideas for new products and pitched those ideas, creating mockups ranging from simple sketches and wireframes to working HTML and CSS. Validated my choices with user feedback, learning the principles of UX design.</p>
      </div>
    </section>
    <aside class="sidebar">
      <div class="tech">
        <h3>Technologies</h3>
        <p>JavaScript, React, React Native, Node, Next.js, Svelte, Ruby on Rails, Vue, HTML, CSS, SCSS, Swift, Objective-C, C#, Xamarin, Python, Java, SQL</p>
      </div>
      <div class="education">
        <h3>Education</h3>
        <h5>University of Minnesota - Twin Cities</h5>
        <p>Computer Science B.A & Journalism B.A.</p>
        <h6 class="gpa">September 2011 - May 2015, GPA 3.3</h6>
      </div>
    </aside>
  </div>
</div>
