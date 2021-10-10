<style>
h1, h2 {
  margin: 0;
}
h1 {
  margin-right: 1em;
  font-size: 2.75em;
}
h2 {
  font-size: 2em;
}
h3 {
  color: var(--main-text-color);
}
h5 {
  font-size: 1.2em;
}
header h2 {
  color: var(--main-theme-color);
}
header a {
  text-decoration: none;
  transition: .3s;
  padding: 0 5px;
}
header p {
  padding: 0 15px;
}
header a:hover {
  color: var(--main-theme-color);
}
.header {
  display: flex;
  color: var(--main-text-color);
  width: 100%;
  padding: 15px;
  align-items: space-between;
  justify-content: space-between;
}
.contact {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: flex-start;
  text-align: right;
  min-width: 400px;
  font-size: 0.8rem;
  font-weight: 600;
}
.contact a {
  color: var(--main-text-color);
}
.body {
  display: flex;
  align-items: flex-start;
  padding: 15px;
}
.main {
  padding-right: 15px;
}
.key {
  margin-top: 3px;
}
.company {
  color: var(--main-text-color);
  font-size: .9em;
}
.job p, .job ul {
  font-size: 1.1em;
}
.job ul li {
  margin: 0;
  padding: 0;
}
.job h4 {
  color: var(--main-theme-color);
}
.job h5 {
  opacity: 0.3;
}
.subjob {
  font-size: 1em;
}
.subjob span {
  opacity: 0.3;
}
.skills {
  font-size: 1rem;
  font-family: var(--main-header-font);
  color: var(--main-theme-color);
  list-style: none;
}
@media(max-width: 1200px) {
  .body {
    flex-direction: column;
  }
  header {
    flex-direction: column;
    align-items: space-between;
  }
}
@media print { 
  p, ul {
    font-size: 0.7em;
    color: var(--main-text-color);
  }
  .job {
    margin-top: 10px;
  }
  .job p, .job ul {
    font-size: 0.65em;
    color: var(--main-text-color);
    margin: 0;
  }
  .contact {
    font-size: 0.5em;
    font-weight: 400;
  }
  .contact span a {
    color: var(--main-text-color);
  }
  .header h2 {
    color: var(--main-text-color);
  }
  .none {
    display: none !important;
  }
  .subjob {
    font-size: 0.7em;
    margin-top: 7px;
  }
  .subjob span {
    opacity: 0.3;
  }
  .job .skills {
    font-size: 0.55rem;
    margin: 0;
    margin-bottom: 5px;
    margin-top: 5px;
  }
  .summary {
    margin: 0;
  }
  h1 {
    font-size: 1.6em;
    color: var(--main-theme-color);
  }
  h2 {
    font-size: 1.4em;
    color: var(--main-text-color);
  }
  h3 {
    font-size: 1em;
    color: var(--main-text-color);
  }
  h4 {
    font-size: 0.85em;
    color: var(--main-theme-color);
  }
  h5 {
    font-size: 0.8em;
    color: var(--main-text-color);
  }
  h6 {
    font-size: 0.6em;
    color: var(--main-text-color);
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
      <div class="contact">
        <span><a href="/">135 Battle Creek Place, Saint Paul, MN 55119</a></span>
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
      </div>
    </div>
    <p class="summary">Software Engineer with over six years of experience creating applications for web, mobile, and Windows. A full-stack developer who aims to help push the internet forward and make it better for everyone. Deeply knowledgeable about the intricacies of JavaScript with a proven ability to learn other tools and languages quickly. Accustomed to vetting new technologies and creating proofs of concept. Excellent at communicating with folks at all levels of technical knowledge and passionate about mentoring.</p>
  </header>
  <div class="body">
    <section class="main">
      <h3>Experience</h3>
      <div class="job">
        <h4>Software Engineer/Consultant <span class="company">/ Daugherty Business Solutions, Bloomington, MN</span></h4>
        <h5>November 2020 - Present</h5>
        <p>Design and implement software systems based on functional specifications at the application, package, class, and method level. Review source code completed by peers and junior developers to ensure adherence to design specs, style guidelines, and best practices. Integrate packages or applications with attention to integration, maintainability, reusability, standards, structure, and efficiency. Participate in Agile ceremonies and other client visible business meetings as part of a team. Perform regression test planning and execution each sprint. Work with operations groups to ensure applications are successfully migrated to production and provide application maintenance and support as required. Leverage tools and methods to understand root cause and recommend options for correction. Provide tutoring for Daugherty University Associate Consultants as needed via Microsoft Teams.</p>
        <h6 class="subjob">Best Buy <span>/ Jun. 2021 - Present</span></h6>
        <p class="key">Lead efforts to clean, modernize and speed up the frontend code. Mentor junior team members on code standards, JavaScript, React, terminal tips and tricks and the industry at large.</p>
        <ul>
          <li>Improve performace of the frontend app by implementing Google Lighthouse standards, code splitting, route-based bundle chunking, and more.</li>
          <li>Rebooted the languishing and unreliable Cypress E2E testing system, getting them set up with Playwright, which handles async/await a lot more smoothly.</li>
          <li>Pushed for thorough code reviews, leading to fewer bugs and an increased understanding among the team of what each other team member is working on.</li>
        </ul>
        <p class="skills">Used: TypeScript, JavaScript, React, Redux, HTML, CSS, Groovy, Spring, SQL</p>
        <h6 class="subjob">Express Scripts <span>/ Nov. 2020 - Jun. 2021</span></h6>
        <p class="key">Helped the team finish work on a large internal application, which is comprised of an API built with Java and Spring Boot and a frontend built with React and Redux. Designed and implemented tests using Jest and Junit for JavaScript and Java respectively.</p>
        <ul>
          <li>Advocated for better development practices within the team, in particular the adoption of automated code styling with Prettier and local Git hooks via Husky.</li>
          <li>Tracked down and troubleshot the most difficult NPM issues, figuring out which packages were not agreeing with each other and why.</li>
          <li>Ran into every onboarding issue in the book and sorted those walkthroughs and hopefully made things easier for the next engineer.</li>
        </ul>
        <p class="skills">Used: JavaScript, React, Redux, HTML, CSS, Java, Spring, SQL</p>
      </div>
      <div class="job">
        <h4>Web Developer <span class="company">/ Minnesota Public Radio, Saint Paul, MN</span></h4>
        <h5>August 2018 - November 2020</h5>
        <p>Maintained American Public Media’s old web applications and built new ones, using everything from server side Node and Rails to frontend React and SCSS. Performed code reviews, mentored new team members and set up automation and guardrails. Proposed new platforms and solutions to increase efficiency and reduce the likelihood of errors as our team continued to shrink.</p>
        <ul>
          <li>Built much of APM's reusable React component libraries and pushed for them to be open source and published on NPM.</li>
          <li>Vetted new tools like Next.js, TypeScript, and React Native, and devised the initial architecture of the apps that ended up using them, then trained in the rest of the team.</li>
          <li>Reworked APM Reports to pass all of Google’s AMP rules so they would more frequently be the top result for the stories they broke. The day Curtis Flowers’ conviction was overturned APM Reports had a record 175K page views.</li>
          <li>Proposed we move to Next.js when we had difficulty getting React c. 2018 and server-side rendering to play nicely. Created a demo that convinced the team this would be more stable in the long run.</li>
          <li>Created the initial version of YourClassical in React Native, proving that we could develop an audio-first app for iOS, Android, and web, then presented it to the Technology Division.</li>
          <li>Proposed that we start tracking tickets on APM's internal GitLab, which was already being paid for and required basically no maintenance, instead of running a separate Redmine server. This saved the Ops team 2-4 hours of support time per sprint.</li>
          <li>Leveraged my journalism and dataviz background to work with the newsroom and revamp our election site. Created new maps and charts for the 2018 and 2020 elections.</li>
        </ul>
        <p class="skills">Used: JavaScript, TypeScript, React, Node, Next.js, HTML, SCSS, Ruby on Rails, GraphQL, PHP</p>
      </div>
      <div class="job">
        <h4>Associate Software Developer <span class="company">/ Design Center Inc., Saint Paul, MN</span></h4>
        <h5>February 2017 - August 2018</h5>
        <p>Helped develop applications for iOS, web, and Windows. Hired as the firm’s first frontend developer, but quickly had to pivot to learning iOS and Windows development to fulfill the company’s actual obligations.</p>
        <ul>
          <li>Worked on a mix of small solo projects and midsize agile projects with a small team.</li>
          <li>Managed client and project manager expectations.</li>
          <li>Wrote the company’s frontend web standards.</li>
          <li>Taught the designers how to write solid HTML and CSS markup and got them set up with an IDE. Stressed to the owner that frontend development, particularly JavaScript development, cannot be offloaded onto designers with no relevant training or interest.</li>
        </ul>
        <p class="skills">Used: Objective-C, Swift, Xamarin, C#, JavaScript, HTML, CSS, PHP</p>
      </div>
      <div class="job">
        <h4>Technology LDP Trainee <span class="company">/ Ameriprise Financial, Saint Paul, MN</span></h4>
        <h5>July 2015 - February 2017</h5>
        <p>Rotated between three different position over the course of 18 months as part of a program for recent graduates.</p>
        <ul>
          <li>Redesigned and wrote the frontend for Ameriprise’s advisor compensation application homepage, working within the limits of the old JSP, IE-only application.</li>
          <li>Tested and polished a client-facing dashboard built with Backbone.js.</li>
          <li>Conducted working sessions to complete disaster recovery plans for all my department’s applications.</li>
        </ul>
        <p class="skills">Used: JavaScript, Backbone.js, HTML, CSS</p>
      </div>
      <div class="job none">
        <h4>Product Strategy & Design Intern <span class="company">/ Pearson VUE, Bloomington, MN</span></h4>
        <h5>May 2014 - Aug 2014</h5>
        <p>Researched ideas for new products and pitched those ideas, creating mockups ranging from simple sketches and wireframes to working HTML and CSS. Validated my choices with user feedback, learning the principles of UX design.</p>
      </div>
    </section>
    <div class="job">
      <h3>Education</h3>
      <h4>Computer Science B.A. & Journalism B.A. <span class="company">/ University of Minnesota - Twin Cities</span></h4>
      <h5>September 2011 - May 2015</h5>
    </div>
  </div>
</div>
