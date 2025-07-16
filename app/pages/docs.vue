<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Navigation -->
    <nav class="bg-white shadow-sm">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center py-4">
          <div class="flex items-center space-x-4">
            <NuxtLink to="/" class="text-blue-600 hover:text-blue-800">
              ← Back to Demo
            </NuxtLink>
            <h1 class="text-xl font-semibold text-gray-900">CardPointe Integration Docs</h1>
          </div>
        </div>
      </div>
    </nav>

    <!-- Main Content -->
    <main class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <div class="bg-white rounded-lg shadow-sm">
        <div class="p-8">
          <!-- Introduction -->
          <section class="mb-12">
            <h2 class="text-3xl font-bold text-gray-900 mb-4">CardPointe Hosted iFrame Integration</h2>
            <p class="text-lg text-gray-600 mb-6">
              This documentation covers the implementation of CardPointe's hosted iframe tokenizer
              with Nuxt 4 and Tailwind CSS for secure, PCI-compliant payment processing.
            </p>
          </section>

          <!-- Features -->
          <section class="mb-12">
            <h3 class="text-2xl font-semibold text-gray-900 mb-4">Features</h3>
            <div class="grid md:grid-cols-2 gap-6">
              <div class="bg-blue-50 p-6 rounded-lg">
                <h4 class="font-semibold text-blue-900 mb-2">🔒 Security</h4>
                <ul class="text-sm text-blue-800 space-y-1">
                  <li>• PCI DSS Level 1 Compliant</li>
                  <li>• End-to-end encryption</li>
                  <li>• Tokenization of sensitive data</li>
                  <li>• Secure iframe communication</li>
                </ul>
              </div>
              <div class="bg-green-50 p-6 rounded-lg">
                <h4 class="font-semibold text-green-900 mb-2">⚡ Performance</h4>
                <ul class="text-sm text-green-800 space-y-1">
                  <li>• Fast tokenization</li>
                  <li>• Minimal JavaScript overhead</li>
                  <li>• Responsive design</li>
                  <li>• Mobile-optimized</li>
                </ul>
              </div>
            </div>
          </section>

          <!-- Setup Instructions -->
          <section class="mb-12">
            <h3 class="text-2xl font-semibold text-gray-900 mb-4">Setup Instructions</h3>
            
            <div class="space-y-6">
              <div>
                <h4 class="text-lg font-semibold text-gray-900 mb-3">1. iFrame Configuration</h4>
                <div class="bg-gray-900 rounded-lg p-4 overflow-x-auto">
                  <code class="text-green-400 text-sm">
                    <!-- Testing URL -->
                    https://fts-uat.cardconnect.com/itoke/ajax-tokenizer.html
                    
                    <!-- Production URL -->
                    https://fts.cardconnect.com/itoke/ajax-tokenizer.html
                  </code>
                </div>
              </div>

              <div>
                <h4 class="text-lg font-semibold text-gray-900 mb-3">2. Parameters</h4>
                <div class="bg-gray-100 rounded-lg p-4">
                  <table class="w-full text-sm">
                    <thead>
                      <tr class="border-b">
                        <th class="text-left py-2">Parameter</th>
                        <th class="text-left py-2">Description</th>
                        <th class="text-left py-2">Default</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr class="border-b">
                        <td class="py-2 font-mono">useexpiry</td>
                        <td class="py-2">Enable expiration date field</td>
                        <td class="py-2">true</td>
                      </tr>
                      <tr class="border-b">
                        <td class="py-2 font-mono">usecvv</td>
                        <td class="py-2">Enable CVV field</td>
                        <td class="py-2">true</td>
                      </tr>
                      <tr class="border-b">
                        <td class="py-2 font-mono">sendcardtypingevent</td>
                        <td class="py-2">Send card type events</td>
                        <td class="py-2">true</td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>

              <div>
                <h4 class="text-lg font-semibold text-gray-900 mb-3">3. Event Handling</h4>
                <div class="bg-gray-900 rounded-lg p-4 overflow-x-auto">
                  <code class="text-green-400 text-sm whitespace-pre">
window.addEventListener('message', (event) => {
  // Ensure message is from CardPointe
  if (!event.origin.includes('cardconnect.com')) return
  
  const data = event.data
  
  if (data.token) {
    // Handle token response
    console.log('Token received:', data.token)
  }
  
  if (data.error) {
    // Handle errors
    console.error('CardPointe error:', data.error)
  }
  
  if (data.type === 'cardtype') {
    // Handle card type detection
    console.log('Card type:', data.cardtype)
  }
})
                  </code>
                </div>
              </div>
            </div>
          </section>

          <!-- Test Cards -->
          <section class="mb-12">
            <h3 class="text-2xl font-semibold text-gray-900 mb-4">Test Card Numbers</h3>
            <div class="grid md:grid-cols-2 gap-4">
              <div class="bg-gray-50 p-4 rounded-lg">
                <h4 class="font-semibold text-gray-900 mb-2">Visa</h4>
                <p class="text-sm text-gray-600 font-mono">4111111111111111</p>
                <p class="text-sm text-gray-600">CVV: 123 | Exp: 12/25</p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg">
                <h4 class="font-semibold text-gray-900 mb-2">MasterCard</h4>
                <p class="text-sm text-gray-600 font-mono">5555555555554444</p>
                <p class="text-sm text-gray-600">CVV: 123 | Exp: 12/25</p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg">
                <h4 class="font-semibold text-gray-900 mb-2">American Express</h4>
                <p class="text-sm text-gray-600 font-mono">378282246310005</p>
                <p class="text-sm text-gray-600">CVV: 1234 | Exp: 12/25</p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg">
                <h4 class="font-semibold text-gray-900 mb-2">Discover</h4>
                <p class="text-sm text-gray-600 font-mono">6011111111111117</p>
                <p class="text-sm text-gray-600">CVV: 123 | Exp: 12/25</p>
              </div>
            </div>
          </section>

          <!-- Token Format -->
          <section class="mb-12">
            <h3 class="text-2xl font-semibold text-gray-900 mb-4">Token Format</h3>
            <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-4">
              <h4 class="font-semibold text-yellow-900 mb-2">CardSecure Token Structure</h4>
              <p class="text-sm text-yellow-800 mb-3">
                CardSecure generates 16-digit tokens based on the following format:
              </p>
              <div class="bg-yellow-100 p-3 rounded font-mono text-sm">
                <p>Original: <span class="text-blue-600">44</span>**********<span class="text-blue-600">9507</span></p>
                <p>Token: <span class="text-red-600">9</span><span class="text-blue-600">44</span>963528741<span class="text-blue-600">9507</span></p>
              </div>
              <ul class="text-sm text-yellow-800 mt-3 space-y-1">
                <li>• "9" prefix (no card brands start with 9)</li>
                <li>• First 2 digits of original card preserved</li>
                <li>• Last 4 digits of original card preserved</li>
                <li>• Middle digits are randomized</li>
              </ul>
            </div>
          </section>

          <!-- Best Practices -->
          <section class="mb-12">
            <h3 class="text-2xl font-semibold text-gray-900 mb-4">Best Practices</h3>
            <div class="grid md:grid-cols-2 gap-6">
              <div>
                <h4 class="font-semibold text-gray-900 mb-3">Security</h4>
                <ul class="text-sm text-gray-600 space-y-2">
                  <li>• Always validate origin of messages</li>
                  <li>• Use HTTPS for all communications</li>
                  <li>• Never store sensitive card data</li>
                  <li>• Implement proper error handling</li>
                  <li>• Use tokenization for recurring payments</li>
                </ul>
              </div>
              <div>
                <h4 class="font-semibold text-gray-900 mb-3">User Experience</h4>
                <ul class="text-sm text-gray-600 space-y-2">
                  <li>• Show loading states during tokenization</li>
                  <li>• Provide clear error messages</li>
                  <li>• Implement responsive design</li>
                  <li>• Add visual security indicators</li>
                  <li>• Support mobile devices</li>
                </ul>
              </div>
            </div>
          </section>

          <!-- Code Example -->
          <section class="mb-12">
            <h3 class="text-2xl font-semibold text-gray-900 mb-4">Implementation Example</h3>
            <div class="bg-gray-900 rounded-lg p-4 overflow-x-auto">
              <code class="text-green-400 text-sm whitespace-pre">
// pages/payment.vue
&lt;template&gt;
  &lt;div class="payment-container"&gt;
    &lt;iframe
      ref="cardPointeIframe"
      :src="iframeUrl"
      @load="onIframeLoad"
      width="100%"
      height="400"
      frameborder="0"
    /&gt;
    
    &lt;button @click="requestToken"&gt;
      Generate Token
    &lt;/button&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script setup&gt;
const cardPointeIframe = ref(null)
const token = ref('')
const iframeUrl = 'https://fts-uat.cardconnect.com/itoke/ajax-tokenizer.html?useexpiry=true&usecvv=true'

const onIframeLoad = () => {
  console.log('iframe loaded')
}

const requestToken = () => {
  cardPointeIframe.value.contentWindow.postMessage('getToken', '*')
}

const handleMessage = (event) => {
  if (event.origin.includes('cardconnect.com') && event.data.token) {
    token.value = event.data.token
  }
}

onMounted(() => {
  window.addEventListener('message', handleMessage)
})

onUnmounted(() => {
  window.removeEventListener('message', handleMessage)
})
&lt;/script&gt;
              </code>
            </div>
          </section>

          <!-- Support -->
          <section>
            <h3 class="text-2xl font-semibold text-gray-900 mb-4">Support & Resources</h3>
            <div class="grid md:grid-cols-2 gap-6">
              <div>
                <h4 class="font-semibold text-gray-900 mb-3">Documentation</h4>
                <ul class="text-sm text-blue-600 space-y-1">
                  <li>• <a href="https://developer.fiserv.com/product/CardPointe" target="_blank" class="hover:underline">CardPointe Developer Portal</a></li>
                  <li>• <a href="https://support.cardpointe.com" target="_blank" class="hover:underline">CardPointe Support Center</a></li>
                  <li>• <a href="https://fts-uat.cardconnect.com/itoke/outer-page.html" target="_blank" class="hover:underline">Live Demo</a></li>
                </ul>
              </div>
              <div>
                <h4 class="font-semibold text-gray-900 mb-3">Environment URLs</h4>
                <ul class="text-sm text-gray-600 space-y-1">
                  <li>• <strong>Testing:</strong> fts-uat.cardconnect.com</li>
                  <li>• <strong>Production:</strong> fts.cardconnect.com</li>
                  <li>• <strong>Support:</strong> support.cardpointe.com</li>
                </ul>
              </div>
            </div>
          </section>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
useHead({
  title: 'CardPointe Integration Documentation',
  meta: [
    { name: 'description', content: 'Complete documentation for CardPointe hosted iframe integration with Nuxt 4' }
  ]
})
</script> 