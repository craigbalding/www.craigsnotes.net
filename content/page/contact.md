+++
date = "2017-06-11T12:42:49+01:00"
title = "contact"
menu = "main"
+++

**Please contact me to introduce yourself, share your thoughts, or anything else. I happily read and reply to every email.**

*The form below is not suitable for very private or confidential information. If you share your contact info, I will get back to you and we can find a better way to communicate.*


<div class="form">
 <form name="contact" action="/" role="form" class="contactForm" netlify>
   <input type="hidden" name="form-name" value="contact">
     <div class="form-group">
       <input type="text" name="name" class="form-control input-text" id="name" placeholder="Your Name" data-rule="minlen:4" data-msg="Please enter at least 4 chars">
       <div class="validation"></div>
     </div>
     <div class="form-group">
       <input type="email" class="form-control input-text" name="email" id="email" placeholder="Your Email" data-rule="email" data-msg="Please enter a valid email">
       <div class="validation"></div>
     </div>
     <div class="form-group">
       <input type="text" class="form-control input-text" name="subject" id="subject" placeholder="Subject" data-rule="minlen:4" data-msg="Please enter at least 8 chars of subject">
       <div class="validation"></div>
     </div>
     <div class="form-group">
        <textarea class="form-control input-text text-area" name="message" rows="5" data-rule="required" data-msg="Please write something for us" placeholder="Message"></textarea>
        <div class="validation"></div>
     </div>
     <div>
     <button>Send</button> <i>  ...and return to the homepage. </i>
   </div>
 </form>
</div>


