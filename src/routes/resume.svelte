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

.header {
  display: flex;
}

.contact {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: space-between;
  text-align: right;
  min-width: 400px;
  font-size: 0.8rem;
  font-weight: 600;
}

.contact a {
  color: var(--main-theme-color);
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
}
</style>

<svelte:head>
  <title>Resume - Kim Thompson</title>
</svelte:head>

<div>
  <header>
    <div class="header">
      <div class="title">
        <h1>Kim Thompson</h1>
        <h2>Software Developer</h2>
      </div>
      <ul class="contact">
        <span>135 Battle Creek Place, Saint Paul, MN 55119</span>
        <span>
          <a href="+1-952-215-7255">
            952-215-7255
          </a>
        </span>
        <span>
          <a href="mailto:kim.thompson.dev@protonmail.com">
            kim.thompson.dev@protonmail.com
          </a>
        </span>
        <span>
          <a href="https://kimthompson.me">
            kimthompson.me
          </a>
        </span>
        <span>
          <a href="https://github.com/kimthompson">
            github.com/kimthompson
          </a>
        </span>
        <span>
          <a href="https://linkedin.com/in/kimberlyannthompson">
            linkedin.com/in/kimberlyannthompson
          </a>
        </span>
      </ul>
    </div>
    <p>Software Engineer with over six years of experience creating applications for web, mobile, and Windows. A full-stack developer who aims to help push the internet forward and make it better for everyone. Deeply knowledgeable about the intricacies of JavaScript with a proven ability to learn other tools and languages quickly. Accustomed to vetting new technologies and creating proofs of concept. Excellent at communicating with folks at all levels of technical knowledge and passionate about mentoring.</p>
  </header>
  <div class="body">
    <section class="main">
      <h3>Experience</h3>
      <div class="job">
        <h4>Software Engineer/Consultant <span class="company">/ Daugherty Business Solutions, Bloomington, MN</span></h4>
        <h5>November 2020 - Present</h5>
        <p>I use my deep React knowledge and the other bits of knowledge I've picked up to help a variety of clients with their tricky projects. Design and implement software systems based on functional specifications at the application, package, class, and method level. Review source code completed by peers and junior developers to ensure adherence to design specs, style guidelines, and best practices. Integrate packages or code applications with attention to integration, maintainability, reusability, standards, structure, and efficiency. Participate in Agile ceremonies and other client visible business meetings as part of a team. Perform regression test planning and execution each sprint. Work with operations groups to ensure applications are successfully migrated to production and provide application maintenance and support as required. Leverage tools and methods to understand root cause and recommend options for correction. Provide tutoring for Daugherty University Associate Consultants as needed via Microsoft Teams.</p>
        <h6 class="key">Key Accomplishments</h6>
        <ul>
          <li><b>Best Buy</b>, <em>Jun. 2021 - Present</em> - React, Redux, Groovy, Spring Boot, JSS</li>
          <li><b>Express Scripts</b>, <em>Nov. 2020 - Jun. 2021</em> - React, Redux, Java, Spring Boot, SCSS</li>
        </ul>
      </div>
      <div class="job">
        <h4>Web Developer <span class="company">/ Minnesota Public Radio, Saint Paul, MN</span></h4>
        <h5>August 2018 - November 2020</h5>
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
        <p>JavaScript, React, React Native, Node, Next.js, Svelte, Java, Spring, SQL, Ruby on Rails, Vue, HTML, CSS, SCSS, Swift, Objective-C, C#, Xamarin, Python</p>
      </div>
      <div class="education">
        <h3>Education</h3>
        <h5>University of Minnesota - Twin Cities</h5>
        <p>Computer Science B.A & Journalism B.A.</p>
        <h6 class="gpa">September 2011 - May 2015</h6>
      </div>
    </aside>
  </div>
</div>
