<script>
import { link } from "svelte-spa-router";

    function testSubmit(e) {
        e.preventDefault();
        alert("Not yet available..")
    }
</script>

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
<div id="contact-div">
    <h2>Get in touch</h2>
    <form onsubmit={testSubmit}>
        <input type="email" placeholder="Your email address" />
        <textarea placeholder="Enter your comment or question.." rows="3" cols="24"></textarea>
        <input type="submit" value="Send" id="submit" />
    </form>
</div>
<a href="/policy" use:link>Terms & Conditions</a>

<div style="margin: 6px;padding: 2px">
    <img src="/sign-warn.svg" alt="disclaimer" width="16" height="16" />
    <span style="font-size: xx-small;">Disclaimer: We strongly advise that you do not make serious, life-decisions based on a coin flip.</span>
</div>
 <style>
    #about-div {
        
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
    @media (max-width:600px) {
        #about-div {
            margin-top:25%;
        }
    }
 </style>
