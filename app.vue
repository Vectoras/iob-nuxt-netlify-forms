<template>
  <div>
    <form name="simple-contact-form" data-netlify="true" method="POST" @submit="handleSubmit">
      <input type="hidden" name="form-name" value="simple-contact-form" />
      <div class="form-row">
        <label for="name" class="form-row__label">Name</label>
        <input type="text" name="name" id="name" class="form-row__input" />
      </div>
      <div class="form-row">
        <label for="email" class="form-row__label">Email</label>
        <input type="email" name="email" id="email" class="form-row__input" />
      </div>
      <div class="form-row">
        <label for="subject" class="form-row__label">Subject</label>
        <input type="text" name="subject" id="subject" class="form-row__input" />
      </div>
      <div class="form-row">
        <label for="message" class="form-row__label">Message</label>
        <textarea name="message" class="form-row__input"></textarea>
      </div>
      <div class="form-row">
        <button type="submit" class="form-row__button">Submit</button>
        <button type="reset" class="form-row__button">Reset</button>
      </div>
    </form>
  </div>
</template>

<script setup lang="ts">
const handleSubmit = (event: SubmitEvent) => {
  event.preventDefault();

  const myForm = event.target;

  // typeguard
  if (!(myForm instanceof HTMLFormElement)) throw new Error("[IOB] The myForm is not a form element !!!");

  const formData = new FormData(myForm);

  fetch("/", {
    method: "POST",
    headers: { "Content-Type": "application/x-www-form-urlencoded" },
    body: new URLSearchParams(formData).toString(),
  })
    .then(() => console.log("form submitted"))
    .catch((error) => alert(error));
};
</script>

<style>
.form-row {
  display: flex;
  gap: 1rem;
  margin: 1rem;
}

.form-row__label {
  width: 5rem;
}

.form-row__input {
  width: 14rem;
  padding: 0.5rem;
}

.form-row__button {
  padding: 0.5rem 1.5rem;
  cursor: pointer;
}
</style>
