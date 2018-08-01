---
type: pages
layout: single
title: Contact Form
author_profile: true
permalink: /contact/
---
If you wish to contact me you can do so by submmiting a message down here, or by sending an email to [alejandro.wurtsss@udlap.mx](mailto:alejandro.wurtsss@udlap.mx)

I will get back to you as soon as possible.

<form name="contact" method="POST" netlify>
  <p>
    <label>Your Name: <input type="text" name="name" /></label>   
  </p>
  <p>
    <label>Your Email: <input type="email" name="email" /></label>
  </p>
  <p>
    <label>Subject: <input type="text" name="subject" /></label>
  </p>
  <p>
    <label>Message: <textarea name="message"></textarea></label>
  </p>
  <p>
    <button type="submit">Send</button>
  </p>
</form>