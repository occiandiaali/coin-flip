<script>
import { link } from "svelte-spa-router";
import milli from "../assets/millionaireodds.png"
import gwd from "../assets/gwd.png"

    function testSubmit(e) {
        e.preventDefault();
        alert("Not yet available..")
    }
</script>

<div id="wrap">
 <div id="about-div">
   
    <h1>About</h1>
    <p>
        The practice of flipping a coin to make decisions can be traced back thousands of years in human history. The ancient Romans practiced a type of coin tossing called "navia aut caput" (ship or head) which was used to settle disputes and make judgments. With time, the coin toss spread across cultures and evolved into a universal symbol of chance.
    </p>
    <p>
        Coin flipping is closely tied to probability theory. A fair coin has two sides, so the theoretical probability of landing on either heads or tails is 50 percent. This makes the coin flip a classic example in statistics for illustrating randomness, probability, and even binary outcomes. Interestingly, while each individual flip is independent, long sequences of flips can produce patterns that spark debate over whether luck or randomness truly governs outcomes. Mathematicians and statisticians have long studied these patterns, using coin flips to teach probability concepts in classrooms worldwide.
    </p>
    <p>In Sports or Games, the coin flip plays a critical role, ensuring fairness in certain competitive scenarios.</p>
    <p><strong>Toss-a-coin</strong> helps you choose between whatever binary options you consider. Every time.</p>
    <p>Give yourself the psychological thrill of chance, while preserving the principles of randomness and fairness.</p>
    <p>Use the default Heads or Tails, or input your own parameters that you want to choose between, and just..flip.</p>
</div>
<hr/>
              <div class="ad-content-div">
        <span>ADVERTISEMENT</span>
        <img
          src={milli}
          alt="millionaireodds"
          width="260px"
          height="42px"
        />
        <span>Are you going to be a Millionaire or Billionaire?</span>
        <span
          >VISIT
          <a
            href="https://millionaireodds.com/"
            target="_blank"
            style="color: black"
            >https://millionaireodds.com</a
          ></span
        >
      </div><hr/>
<div id="contact-div">
    <h2>Feedback</h2>
    <form onsubmit={testSubmit}>
        <input type="email" placeholder="Your email address" />
        <textarea placeholder="Enter your comment or question.." rows="3" cols="24"></textarea>
        <input type="submit" value="Send" id="submit" />
    </form>
</div>
          <div class="ad-content-div">
        <span>ADVERTISEMENT</span>
        <img
          src={gwd}
          alt="guesswhodaily"
          width="260px"
          height="42px"
        />
        <span>Your daily celebrity puzzle</span>
        <span
          >VISIT
          <a
            href="https://guesswhodaily.online/"
            target="_blank"
            style="color: black"
            >https://guesswhodaily.online</a
          ></span
        >
      </div>
      <hr/>
<a href="/policy" use:link style="color: wheat;">Terms & Conditions</a>

<div style="margin: 6px;padding: 2px">
    <img src="/sign-warn.svg" alt="disclaimer" width="16" height="16" />
    <span style="font-size: xx-small;">This website is purely for entertainment purposes.</span>
</div>

</div>
 <style>
 #wrap {

/* background: #660291;
background: linear-gradient(0deg, #660291, #DFCCFF); */
background: #584f5c;
background: linear-gradient(90deg, #584f5c, #DFCCFF);
color: black;
        padding: 6px;
 }

    #contact-div form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-top: 3%;
        padding: 6px;
    }
    #submit {
        background-color: black;
        color: white;
        margin: 4px;
        padding: 6px;
        border: none;
        cursor: pointer;
    }
    input, textarea {
        padding: 8px;
        margin: 4px;
    }
     .ad-content-div {
        width: 320px;
        height: auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        border-radius: 6x;
        color: rgb(179, 175, 175);
      }
  .ad-content-div span {
    font-size: small;
  }  
    @media (max-width:600px) {
        #about-div {
            margin-top:25%;
        }
    }
 </style>
