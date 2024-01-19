<template>
  <section id="contact-us">
    <h1>Get in Touch!</h1>

    <!-- contact info -->
    <div class="container">
      <div class="contact-info">
        <div class="specific-info">
          <i class="fas fa-home"></i>
          <div>
            <p class="title">City El Ons</p>
            <p class="subtitle"> Avenue</p>
          </div>
        </div>
        <div class="specific-info">
          <i class="fas fa-phone-alt"></i>
          <div>
            <a href="tel:+254720XXXXXX">+216 457 400  </a>
            <br />
            <a href="tel:+254721XXXXXX">+216 721 800 </a>

            <p class="subtitle">Mon to Fri 9am-6pm</p>
          </div>
        </div>
        <div class="specific-info">
          <i class="fas fa-envelope-open-text"></i>
          <div>
            <a href="mailto:info@alphayo.co.ke">
              <p class="title">HarmoniBlog@gmail.com</p>
            </a>
            <p class="subtitle">Send us your query anytime!</p>
          </div>
        </div>
      </div>

      <!-- Contact Form -->
      <div class="contact-form">
        <form action="#" method="post">
          <!-- Name -->
          <label for="name"><span>Name</span></label>
          <input type="text" id="name" name="name" v-model="formData.name" />

          <!-- Email -->
          <label for="email"><span>Email</span></label>
          <input type="text" id="email" name="email" v-model="formData.email" />

          <!-- Subject -->
          <label for="subject"><span>Subject</span></label>
          <input type="text" id="subject" name="subject" v-model="formData.subject" />

          <!-- Message -->
          <label for="message"><span>Message</span></label>
          <textarea id="message" name="message" v-model="formData.message"></textarea>

          <!-- Button -->
          <input type="submit" value="Submit" @click.prevent="submitForm" />
        </form>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        subject: '',
        message: ''
      }
    };
  },
  methods: {
    submitForm() {
      // Ajoutez votre logique pour traiter le formulaire ici
      console.log('Form submitted!', this.formData);
      // Réinitialisez les valeurs du formulaire après l'envoi
    this.formData.name = '';
    this.formData.email = '';
    this.formData.subject = '';
    this.formData.message = '';
  
    }
  }
};
</script>

<style scoped>
/* Ajoutez vos styles CSS ici */
</style>
