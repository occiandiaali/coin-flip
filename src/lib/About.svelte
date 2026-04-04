<script>
import { link } from "svelte-spa-router";

    function testSubmit(e) {
        e.preventDefault();
        alert("Not yet available..")
    }
</script>

 <div id="about-div">
   
    <h1 style="margin-top: 25%;">About Us</h1>
    <p>
        Have you ever found yourself torn between two options?
          
    </p>
    <p>
    Leave, or Stay?
    </p>
        <p>
    Buy, or Sell?
    </p>
        <p>
    Fish, or Eggs?
    </p>
        <p>
    James, or John?
    </p>

    <p>Sometimes, we'd rather not bear the burden of deciding for ourselves. Right?</p>
    <p>
        The flip of a coin is a completely random event, and "random" simply means "unpredictable".
        Well, how about just flipping a coin to decide?
    </p>
    <p><strong>Coin Flip</strong> helps you choose between options. Every time.</p>
    <p>Use the default Heads or Tails, or input your own parameters that you want to choose between, and just..flip.</p>
</div>
<div id="contact-div">
    <h2>Get in touch</h2>
    <form onsubmit={testSubmit}>
        <input type="email" placeholder="Your email address" />
        <textarea placeholder="Enter your comment or question.." rows="4" cols="28"></textarea>
        <input type="submit" value="Send" id="submit" />
    </form>
</div>
<a href="/policy" use:link>Terms & Conditions</a>

<div style="margin: 6px;padding: 4px">
    <img src="/sign-warn.svg" alt="disclaimer" width="16" height="16" />
    <span style="font-size: xx-small;">Disclaimer: We strongly advise that you do not make serious decisions based on a coin flip.</span>
</div>
 <style>
    #about-div {
        
        padding: 6px;
    }
        #contact-div {
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
    @media (max-width:600px) {
        #about-div {
            margin-top: 3%;
        }
    }
 </style>
