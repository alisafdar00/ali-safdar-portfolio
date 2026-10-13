
<template>
  <section id="contact" class="bg-black text-white py-20 px-6">
    <div class="max-w-3xl mx-auto">

      <h2 class="text-4xl font-bold text-center mb-4">
        Contact <span class="text-blue-500">Me</span>
      </h2>

      <p class="text-gray-400 text-center mb-10">
        Have a project or job opportunity? Send me a message.
      </p>

      <form
        @submit.prevent="sendEmail"
        class="bg-gray-900 border border-gray-800
               rounded-2xl p-6 md:p-8 space-y-5"
      >
        <div>
          <label class="block mb-2 text-sm">Your Name</label>
          <input
            v-model.trim="form.from_name"
            type="text"
            required
            maxlength="100"
            autocomplete="name"
            placeholder="Enter your name"
            class="w-full rounded-lg bg-black border border-gray-700
                   p-3 text-white outline-none focus:border-blue-500"
          />
        </div>

        <div>
          <label class="block mb-2 text-sm">Your Email</label>
          <input
            v-model.trim="form.from_email"
            type="email"
            required
            maxlength="254"
            autocomplete="email"
            placeholder="Enter your email"
            class="w-full rounded-lg bg-black border border-gray-700
                   p-3 text-white outline-none focus:border-blue-500"
          />
        </div>

        <div>
          <label class="block mb-2 text-sm">Subject</label>
          <input
            v-model.trim="form.subject"
            type="text"
            required
            maxlength="150"
            placeholder="Job opportunity / Project inquiry"
            class="w-full rounded-lg bg-black border border-gray-700
                   p-3 text-white outline-none focus:border-blue-500"
          />
        </div>

        <div>
          <label class="block mb-2 text-sm">Message</label>
          <textarea
            v-model.trim="form.message"
            rows="5"
            required
            minlength="10"
            maxlength="2000"
            placeholder="Write your message here..."
            class="w-full rounded-lg bg-black border border-gray-700
                   p-3 text-white outline-none focus:border-blue-500"
          ></textarea>
        </div>

        <p
          v-if="successMessage"
          role="status"
          aria-live="polite"
          class="text-green-400"
        >
          {{ successMessage }}
        </p>

        <p
          v-if="errorMessage"
          role="alert"
          class="text-red-400"
        >
          {{ errorMessage }}
        </p>

        <button
          type="submit"
          :disabled="loading"
          class="w-full bg-blue-600 hover:bg-blue-700
                 disabled:opacity-50 disabled:cursor-not-allowed
                 text-white font-semibold py-3 rounded-lg transition"
        >
          {{ loading ? 'Sending...' : 'Send Message' }}
        </button>
      </form>
    </div>
  </section>
</template>

<script>
import emailjs from '@emailjs/browser'

export default {
  name: 'Contact',

  data() {
    return {
      form: {
        from_name: '',
        from_email: '',
        subject: '',
        message: ''
      },

      loading: false,
      successMessage: '',
      errorMessage: ''
    }
  },

  methods: {
    async sendEmail() {
      if (this.loading) return

      this.loading = true
      this.successMessage = ''
      this.errorMessage = ''

      try {
        const serviceID = import.meta.env.VITE_EMAILJS_SERVICE_ID
        const templateID = import.meta.env.VITE_EMAILJS_TEMPLATE_ID
        const publicKey = import.meta.env.VITE_EMAILJS_PUBLIC_KEY
        
        if (!serviceID || !templateID || !publicKey) {
          throw new Error('Email configuration is missing.')
        }

        await emailjs.send(
          serviceID,
          templateID,
          {
            from_name: this.form.from_name,
            from_email: this.form.from_email,
            subject: this.form.subject,
            message: this.form.message,
            reply_to: this.form.from_email
          },
          {
            publicKey: publicKey
          }
        )

        this.successMessage =
          'Your message has been sent successfully!'

        this.form = {
          from_name: '',
          from_email: '',
          subject: '',
          message: ''
        }
      } catch (error) {
        console.error('Email sending failed:', error)

        this.errorMessage =
          'Sorry, your message could not be sent. Please try again.'
      } finally {
        this.loading = false
      }
    }
  }
}
</script>
