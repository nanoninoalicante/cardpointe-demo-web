<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100">
    <!-- Header -->
    <header class="bg-white shadow-sm">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center py-6">
          <div class="flex items-center">
            <h1 class="text-2xl font-bold text-gray-900">CardPointe Demo</h1>
          </div>
          <div class="flex items-center space-x-4">
            <NuxtLink
              to="/docs"
              class="text-sm text-blue-600 hover:text-blue-800"
            >
              📚 Documentation
            </NuxtLink>
            <span class="text-sm text-gray-500">Test Environment</span>
            <div class="h-2 w-2 bg-green-400 rounded-full"></div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content -->
    <main class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
      <!-- Hero Section -->
      <div class="text-center mb-12">
        <h2 class="text-4xl font-bold text-gray-900 mb-4">
          Secure Payment Processing
        </h2>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto">
          Experience CardPointe's hosted iframe tokenizer for secure,
          PCI-compliant payment processing
        </p>
      </div>

      <!-- Configuration Panel -->
      <div class="bg-white rounded-xl shadow-lg overflow-hidden mb-8">
        <div class="p-6">
          <div class="flex items-center justify-between mb-4">
            <h3 class="text-lg font-semibold text-gray-900">
              iFrame Configuration
            </h3>
            <button
              @click="showConfig = !showConfig"
              class="text-sm text-blue-600 hover:text-blue-800 flex items-center"
            >
              <span>{{ showConfig ? "Hide" : "Show" }} Config</span>
              <svg
                class="ml-1 h-4 w-4 transform transition-transform"
                :class="{ 'rotate-180': showConfig }"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M19 9l-7 7-7-7"
                ></path>
              </svg>
            </button>
          </div>

          <div v-if="showConfig" class="space-y-6">
            <!-- Input Formatting -->
            <div>
              <h4 class="font-medium text-gray-900 mb-3">Input Formatting</h4>
              <div class="grid md:grid-cols-2 gap-4">
                <div class="flex items-center space-x-2">
                  <input
                    id="formatinput"
                    v-model="cardPointeConfig.formatinput"
                    type="checkbox"
                    class="rounded border-gray-300"
                  />
                  <label for="formatinput" class="text-sm text-gray-700">
                    Format Card Number (spaces every 4 digits)
                  </label>
                </div>

                <div class="flex items-center space-x-2">
                  <input
                    id="maskfirsttwo"
                    v-model="cardPointeConfig.maskfirsttwo"
                    type="checkbox"
                    class="rounded border-gray-300"
                  />
                  <label for="maskfirsttwo" class="text-sm text-gray-700">
                    Mask First 2 Digits
                  </label>
                </div>
              </div>
            </div>

            <!-- Input Labels -->
            <div class="border-t pt-6">
              <h4 class="font-medium text-gray-900 mb-3">Input Labels</h4>
              <div class="grid md:grid-cols-2 gap-4">
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">
                    Card Number Label
                  </label>
                  <input
                    v-model="cardPointeConfig.cardlabel"
                    type="text"
                    class="w-full border border-gray-300 rounded-md px-3 py-2 text-sm"
                  />
                </div>

                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">
                    Card Number Title (Accessibility)
                  </label>
                  <input
                    v-model="cardPointeConfig.cardtitle"
                    type="text"
                    class="w-full border border-gray-300 rounded-md px-3 py-2 text-sm"
                  />
                </div>

                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">
                    CVV Label
                  </label>
                  <input
                    v-model="cardPointeConfig.cvvlabel"
                    type="text"
                    class="w-full border border-gray-300 rounded-md px-3 py-2 text-sm"
                  />
                </div>

                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">
                    CVV Title (Accessibility)
                  </label>
                  <input
                    v-model="cardPointeConfig.cvvtitle"
                    type="text"
                    class="w-full border border-gray-300 rounded-md px-3 py-2 text-sm"
                  />
                </div>

                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">
                    Expiry Label
                  </label>
                  <input
                    v-model="cardPointeConfig.expirylabel"
                    type="text"
                    class="w-full border border-gray-300 rounded-md px-3 py-2 text-sm"
                  />
                </div>

                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">
                    Expiry Month Title
                  </label>
                  <input
                    v-model="cardPointeConfig.expirymonthtitle"
                    type="text"
                    class="w-full border border-gray-300 rounded-md px-3 py-2 text-sm"
                  />
                </div>

                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">
                    Expiry Year Title
                  </label>
                  <input
                    v-model="cardPointeConfig.expiryyeartitle"
                    type="text"
                    class="w-full border border-gray-300 rounded-md px-3 py-2 text-sm"
                  />
                </div>
              </div>
            </div>

            <!-- Styling Options -->
            <div class="border-t pt-6">
              <h4 class="font-medium text-gray-900 mb-3">Styling Options</h4>
              <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-4">
                <!-- Input Field Styling -->
                <div class="space-y-3">
                  <h5 class="text-sm font-medium text-gray-700">
                    Input Fields
                  </h5>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Background Color</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputBackground"
                      type="color"
                      class="w-full h-8 border border-gray-300 rounded cursor-pointer"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Border Color</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputBorder"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="1px solid #d1d5db"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Border Radius</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputBorderRadius"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="6px"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Padding</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputPadding"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="8px 12px"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Font Size</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputFontSize"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="14px"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Text Color</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputTextColor"
                      type="color"
                      class="w-full h-8 border border-gray-300 rounded cursor-pointer"
                    />
                  </div>
                </div>

                <!-- Focus State Styling -->
                <div class="space-y-3">
                  <h5 class="text-sm font-medium text-gray-700">Focus State</h5>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Focus Border</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputFocusBorder"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="2px solid #3b82f6"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Focus Shadow</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.inputFocusBoxShadow"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="0 0 0 3px rgba(59, 130, 246, 0.1)"
                    />
                  </div>
                </div>

                <!-- Label Styling -->
                <div class="space-y-3">
                  <h5 class="text-sm font-medium text-gray-700">Labels</h5>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Label Color</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.labelColor"
                      type="color"
                      class="w-full h-8 border border-gray-300 rounded cursor-pointer"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Label Font Size</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.labelFontSize"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="14px"
                    />
                  </div>

                                     <div>
                     <label class="block text-xs text-gray-600 mb-1"
                       >Label Weight</label
                     >
                     <select
                       v-model="cardPointeConfig.styling.labelFontWeight"
                       class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                     >
                       <option value="normal">Normal</option>
                       <option value="500">Medium</option>
                       <option value="600">Semi-bold</option>
                       <option value="700">Bold</option>
                     </select>
                   </div>
                   
                   <div>
                     <label class="block text-xs text-gray-600 mb-1"
                       >Label Margin Top</label
                     >
                     <input
                       v-model="cardPointeConfig.styling.labelMarginTop"
                       type="text"
                       class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                       placeholder="8px"
                     />
                   </div>
                </div>

                <!-- Error Styling -->
                <div class="space-y-3">
                  <h5 class="text-sm font-medium text-gray-700">
                    Error Messages
                  </h5>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Error Color</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.errorColor"
                      type="color"
                      class="w-full h-8 border border-gray-300 rounded cursor-pointer"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Error Font Size</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.errorFontSize"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="12px"
                    />
                  </div>
                </div>

                <!-- Layout Styling -->
                <div class="space-y-3">
                  <h5 class="text-sm font-medium text-gray-700">Layout</h5>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Container Background</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.containerBackground"
                      type="color"
                      class="w-full h-8 border border-gray-300 rounded cursor-pointer"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Container Padding</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.containerPadding"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="16px"
                    />
                  </div>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Field Spacing</label
                    >
                    <input
                      v-model="cardPointeConfig.styling.fieldMarginBottom"
                      type="text"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1"
                      placeholder="16px"
                    />
                  </div>
                </div>

                <!-- Custom CSS -->
                <div class="space-y-3">
                  <h5 class="text-sm font-medium text-gray-700">Custom CSS</h5>

                  <div>
                    <label class="block text-xs text-gray-600 mb-1"
                      >Additional CSS</label
                    >
                    <textarea
                      v-model="cardPointeConfig.customCss"
                      rows="4"
                      class="w-full text-xs border border-gray-300 rounded px-2 py-1 font-mono"
                      placeholder=".error { color: red; }"
                    ></textarea>
                  </div>
                </div>
              </div>
            </div>

            <!-- URL Preview -->
            <div class="border-t pt-6">
              <h4 class="font-medium text-gray-900 mb-3">
                Generated URL Preview
              </h4>
              <div class="bg-gray-50 p-4 rounded-lg">
                <code class="text-sm text-gray-800 break-all">{{
                  iframeUrl
                }}</code>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Payment Form Container -->
      <div class="bg-white rounded-xl shadow-xl overflow-hidden">
        <div class="p-8">
          <div class="flex items-center justify-between mb-8">
            <h3 class="text-2xl font-semibold text-gray-900">
              Payment Details
            </h3>
            <div class="flex items-center space-x-2">
              <svg
                class="h-5 w-5 text-green-500"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                ></path>
              </svg>
              <span class="text-sm text-gray-600">SSL Secured</span>
            </div>
          </div>

          <!-- Payment Form -->
          <form
            @submit.prevent="processPayment"
            class="space-y-6"
            name="tokenform"
            id="tokenform"
          >
            <!-- Hidden inputs for token and expiry storage -->
            <input type="hidden" name="mytoken" id="mytoken" :value="token" />
            <input type="hidden" name="expiry" id="expiry" :value="expiry" />

            <!-- Order Summary -->
            <div class="bg-gray-50 rounded-lg p-6">
              <h4 class="font-semibold text-gray-900 mb-4">Order Summary</h4>
              <div class="flex justify-between items-center mb-2">
                <span class="text-gray-600">Sample Product</span>
                <span class="text-gray-900">$29.99</span>
              </div>
              <div class="flex justify-between items-center mb-2">
                <span class="text-gray-600">Tax</span>
                <span class="text-gray-900">$2.70</span>
              </div>
              <div class="border-t pt-2 mt-4">
                <div
                  class="flex justify-between items-center font-semibold text-lg"
                >
                  <span>Total</span>
                  <span class="text-green-600">$32.69</span>
                </div>
              </div>
            </div>

            <div class="bg-gray-50 rounded-lg p-6">
              <h4 class="font-semibold text-gray-900 mb-4">Customer Payment Information</h4>
              
              <!-- Card Holder Name -->
              <div class="mb-4">
                <label for="cardHolderName" class="block text-sm font-medium text-gray-700 mb-2">
                  Card Holder Name
                </label>
                <input
                  id="cardHolderName"
                  v-model="cardHolderName"
                  type="text"
                  name="cardHolderName"
                  class="w-full border-2 border-gray-300 rounded-lg px-4 py-3 text-gray-900 focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200 transition-colors"
                  placeholder="Enter full name as shown on card"
                  required
                />
              </div>

              <!-- Street Number and Zip Code -->
              <div class="grid grid-cols-3 gap-4 mb-4">
                <!-- Street Number -->
                                  <div class="col-span-2">
                    <label for="streetNumber" class="block text-sm font-medium text-gray-700 mb-2">
                      Street Address and Number
                    </label>
                  <input
                    id="streetNumber"
                    v-model="streetNumber"
                    type="text"
                    name="streetNumber"
                    class="w-full border-2 border-gray-300 rounded-lg px-4 py-3 text-gray-900 focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200 transition-colors"
                    placeholder="Enter street address"
                    required
                  />
                </div>

                <!-- Zip Code -->
                <div class="col-span-1">
                  <label for="zipCode" class="block text-sm font-medium text-gray-700 mb-2">
                    Zip Code
                  </label>
                  <input
                    id="zipCode"
                    v-model="zipCode"
                    type="text"
                    name="zipCode"
                    class="w-full border-2 border-gray-300 rounded-lg px-4 py-3 text-gray-900 focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200 transition-colors"
                    placeholder="12345"
                    pattern="[0-9]{5}(-[0-9]{4})?"
                    required
                  />
                </div>
              </div>
            </div>

            <!-- CardPointe Hosted iFrame -->
            <div class="space-y-4">
              <label class="block text-sm font-medium text-gray-700">
                Payment Information
              </label>

              <!-- iframe Container with Loading Overlay -->
              <div class="relative">
                <iframe
                  ref="cardPointeIframe"
                  :src="iframeUrl"
                  id="tokenFrame"
                  name="tokenFrame"
                  width="100%"
                  height="350"
                  frameborder="0"
                  class="rounded-lg border border-gray-200"
                  @load="onIframeLoad"
                />

                <!-- Loading Overlay -->
                <div
                  v-if="isLoading"
                  class="absolute inset-0 flex items-center justify-center bg-gray-100 rounded-lg"
                >
                  <div
                    class="animate-spin rounded-full h-8 w-8 border-b-2 border-blue-600"
                  ></div>
                  <span class="ml-2 text-gray-600"
                    >Loading secure payment form...</span
                  >
                </div>

                <!-- Overlay for additional security indication -->
                <div
                  class="absolute top-4 right-4 bg-green-100 text-green-800 px-3 py-1 rounded-full text-xs font-medium"
                >
                  🔒 PCI Compliant
                </div>
              </div>
            </div>

            <!-- Token Display (for demo purposes) -->
            <div
              v-if="token"
              class="bg-green-50 border border-green-200 rounded-lg p-4"
            >
              <h4 class="font-semibold text-green-900 mb-2">
                Token Generated Successfully!
              </h4>
              <div class="text-sm text-green-800">
                <p><strong>Token:</strong> {{ token }}</p>
                <p><strong>Expiry:</strong> {{ expiry }}</p>
                <p class="mt-1 text-green-600">
                  This token can now be used for secure payment processing
                </p>
              </div>
            </div>

            <!-- Error Display -->
            <div
              v-if="error"
              class="bg-red-50 border border-red-200 rounded-lg p-4"
            >
              <h4 class="font-semibold text-red-900 mb-2">Error</h4>
              <p class="text-sm text-red-800">{{ error }}</p>
            </div>

            <!-- Action Button -->
            <div class="flex">
              <button
                type="submit"
                :disabled="!token || isProcessing"
                class="w-full bg-green-600 text-white py-3 px-6 rounded-lg font-semibold hover:bg-green-700 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
              >
                <span
                  v-if="isProcessing"
                  class="flex items-center justify-center"
                >
                  <div
                    class="animate-spin rounded-full h-4 w-4 border-b-2 border-white mr-2"
                  ></div>
                  Processing...
                </span>
                <span v-else>Complete Payment</span>
              </button>
            </div>
          </form>
        </div>
      </div>

      <!-- Test Cards -->
      <div class="mt-12 bg-white rounded-lg shadow-sm p-6">
        <h3 class="text-lg font-semibold text-gray-900 mb-4">
          Test Card Numbers
        </h3>
        <div class="grid md:grid-cols-2 gap-4">
          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-semibold text-gray-900 mb-2">💳 Visa</h4>
            <p class="text-sm text-gray-600 font-mono">4111111111111111</p>
            <p class="text-sm text-gray-600">CVV: 123 | Exp: 12/25</p>
          </div>
          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-semibold text-gray-900 mb-2">💳 MasterCard</h4>
            <p class="text-sm text-gray-600 font-mono">5555555555554444</p>
            <p class="text-sm text-gray-600">CVV: 123 | Exp: 12/25</p>
          </div>
          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-semibold text-gray-900 mb-2">
              💳 American Express
            </h4>
            <p class="text-sm text-gray-600 font-mono">378282246310005</p>
            <p class="text-sm text-gray-600">CVV: 1234 | Exp: 12/25</p>
          </div>
          <div class="bg-gray-50 p-4 rounded-lg">
            <h4 class="font-semibold text-gray-900 mb-2">💳 Discover</h4>
            <p class="text-sm text-gray-600 font-mono">6011111111111117</p>
            <p class="text-sm text-gray-600">CVV: 123 | Exp: 12/25</p>
          </div>
        </div>
      </div>

      <!-- Integration Info -->
      <div class="mt-8 bg-white rounded-lg shadow-sm p-6">
        <h3 class="text-lg font-semibold text-gray-900 mb-4">
          Integration Details
        </h3>
        <div class="grid md:grid-cols-2 gap-6">
          <div>
            <h4 class="font-medium text-gray-900 mb-2">Test Environment</h4>
            <p class="text-sm text-gray-600">
              This demo uses CardPointe's test environment. Use test card
              numbers for testing.
            </p>
          </div>
          <div>
            <h4 class="font-medium text-gray-900 mb-2">Security Features</h4>
            <ul class="text-sm text-gray-600 space-y-1">
              <li>• PCI DSS Level 1 Compliant</li>
              <li>• End-to-end encryption</li>
              <li>• Tokenization</li>
              <li>• Fraud protection</li>
            </ul>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch, computed } from "vue";

// Page meta
useHead({
  title: "CardPointe Demo - Hosted iFrame Integration",
  meta: [
    {
      name: "description",
      content:
        "CardPointe hosted iframe tokenizer demo with Nuxt 4 and Tailwind CSS",
    },
  ],
});

// Reactive state
const isLoading = ref(true);
const isProcessing = ref(false);
const token = ref("");
const expiry = ref("");
const error = ref("");
const cardPointeIframe = ref(null);
const showConfig = ref(false);
const cardHolderName = ref("");
const streetNumber = ref("");
const zipCode = ref("");

// CardPointe iframe configuration
const cardPointeConfig = ref({
  // Base URL for the iframe tokenizer
  baseUrl: "https://boltgw-uat.cardconnect.com/itoke/ajax-tokenizer.html",

  // Basic options
  useexpiry: true, // Collect expiration date
  usecvv: true, // Collect CVV/CVC

  // Focus and Input Controls
  autofocus: true, // If true, the input field will be focused when the page loads
  cardinputmaxlength: 2000, // Controls the maximum character limit for the card number field
  cardnumbernumericonly: false, // If true, the card number input field ignores non-numeric values

  // Input Formatting
  formatinput: true, // Styles card number to be separated every four numbers
  maskfirsttwo: false, // If true, the first 2 digits of the card number are masked

  // Input Labels
  cardlabel: "Card Number", // Controls the text inside the label for the card number field
  cardtitle: "Credit Card Number", // Controls the title and aria-label HTML attributes for card number input
  cvvlabel: "CVV", // Controls the text inside the label for the CVV field
  cvvtitle: "Card Verification Value", // Controls the title and aria-label HTML attributes for CVV input
  expirylabel: "Expiration Date", // Controls the text inside the label for the expiration date selectors
  expirymonthtitle: "Expiration Month", // Controls the title and aria-label HTML attributes for expiry month
  expiryyeartitle: "Expiration Year", // Controls the title and aria-label HTML attributes for expiry year

  // CSS Styling Options
  customCss: "", // Custom CSS string (will be URL encoded automatically)

     // Pre-built styling options (will be combined into CSS)
   styling: {
     // Input field styling
     inputBackground: "#ffffff", // Background color for input fields
     inputBorder: "2px solid #e5e7eb", // Modern thicker border
     inputBorderRadius: "12px", // More rounded corners
     inputPadding: "16px 20px", // Generous padding for better UX
     inputFontSize: "16px", // Optimal font size for readability
     inputFontFamily: "-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif", // Modern font stack
     inputTextColor: "#1f2937", // Darker text for better contrast
    //  inputWidth: "100%", // Width of input fields
     inputHeight: "56px", // Comfortable height following Material Design

     // Focus state styling
     inputFocusBorder: "2px solid #3b82f6", // Blue focus border
     inputFocusOutline: "none", // Remove default outline
     inputFocusBoxShadow: "0 0 0 4px rgba(59, 130, 246, 0.1), 0 1px 3px rgba(0, 0, 0, 0.1)", // Enhanced focus shadow with depth

     // Label styling
     labelColor: "#1f2937", // Darker label color for better hierarchy
     labelFontSize: "14px", // Slightly larger labels
     labelFontWeight: "600", // Semi-bold for better readability
     labelMarginTop: "8px", // No top margin for cleaner look
     labelMarginBottom: "6px", // Consistent spacing below labels

     // Error styling
     errorColor: "#dc2626", // Modern red error color
     errorFontSize: "13px", // Slightly larger error text
     errorMarginTop: "6px", // Better spacing above errors

     // Layout styling
     fieldMarginBottom: "24px", // More generous spacing between fields
     containerPadding: "24px", // More padding for breathing room
     containerBackground: "#fafafa", // Very light gray background for subtle depth

     // Select dropdown styling (for expiry date)
     selectBackground: "#ffffff", // White background for selects
     selectBorder: "2px solid #e5e7eb", // Matching border with inputs
     selectBorderRadius: "12px", // Matching border radius
     selectPadding: "16px 20px", // Matching padding
     selectFontSize: "16px", // Matching font size
     selectTextColor: "#1f2937", // Matching text color
   },

  // Response Options
  enhancedresponse: true, // If true, includes additional parameters in JSON response (token, errorCode, errorMessage)

  // Mobile Options
  fullmobilekeyboard: false, // Displays full alphanumeric keyboard in mobile browsers (for ACH input)

  // Timing Controls
  inactivityto: 500, // How long (ms) to wait after onInput event before considering input complete
  selectinputdelay: 0, // Delay (ms) to ignore input to newly selected field (iOS fix)

  // Event Options
  sendcardtypingevent: true, // Send event when user begins entering card number
  invalidcreditcardevent: true, // Send event when card number is invalid (use instead of invalidinputevent with usecvv/useexpiry)
  invalidcvvevent: true, // Send event when CVV is invalid (requires usecvv=true)
  invalidexpiryevent: true, // Send event when expiry is invalid (requires useexpiry=true)
  invalidinputevent: true, // Send event when card number is invalid (use when only card number required)

  // Layout Options
  orientation: "default", // Controls orientation: default, horizontal, vertical, custom

  // Swipe Device Options
  swipeonly: false, // If true, only swipe input allowed (clears manual input)
  swiperate: 0.2, // Threshold for determining swipe vs typing (characters per ms)

  // Mobile Tokenization
  tokenizewheninactive: false, // Perform tokenization when input stops (for mobile)

  // Token Options
  tokenpropname: "message", // Name of token property in JSON message
  unique: false, // If true, generates unique token for each tokenization
});

// Function to generate CSS from styling options
const generateCss = () => {
  const styling = cardPointeConfig.value.styling;
  const customCss = cardPointeConfig.value.customCss;

  let css = "";

  // Input field styling - targeting specific CardPointe elements
  css += `#ccnumfield, #cccvvfield, input[type="tel"], input[type="text"], input[type="number"] {
    background-color: ${styling.inputBackground};
    border: ${styling.inputBorder};
    border-radius: ${styling.inputBorderRadius};
    padding: ${styling.inputPadding};
    font-size: ${styling.inputFontSize};
    font-family: ${styling.inputFontFamily};
         color: ${styling.inputTextColor};
     height: ${styling.inputHeight};
    box-sizing: border-box;
    transition: all 0.2s ease-in-out;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  }`;

  // Hover state styling
  css += `#ccnumfield:hover, #cccvvfield:hover, input[type="tel"]:hover, input[type="text"]:hover, input[type="number"]:hover {
    border-color: #9ca3af;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }`;

  // Focus state styling
  css += `#ccnumfield:focus, #cccvvfield:focus, input[type="tel"]:focus, input[type="text"]:focus, input[type="number"]:focus {
    border: ${styling.inputFocusBorder};
    outline: ${styling.inputFocusOutline};
    box-shadow: ${styling.inputFocusBoxShadow};
  }`;

  // Disabled state styling
  css += `#ccnumfield:disabled, #cccvvfield:disabled, input[type="tel"]:disabled, input[type="text"]:disabled, input[type="number"]:disabled {
    background-color: #f3f4f6;
    border-color: #d1d5db;
    color: #9ca3af;
    cursor: not-allowed;
    opacity: 0.6;
  }`;

  // Select dropdown styling - targeting specific CardPointe elements
  css += `#ccexpirymonth, #ccexpiryyear, select {
    background-color: ${styling.selectBackground};
    border: ${styling.selectBorder};
    border-radius: ${styling.selectBorderRadius};
    padding: ${styling.selectPadding};
    font-size: ${styling.selectFontSize};
    color: ${styling.selectTextColor};
    box-sizing: border-box;
    transition: all 0.2s ease-in-out;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    cursor: pointer;
  }`;

  // Select hover state
  css += `#ccexpirymonth:hover, #ccexpiryyear:hover, select:hover {
    border-color: #9ca3af;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }`;

  // Select focus state
  css += `#ccexpirymonth:focus, #ccexpiryyear:focus, select:focus {
    border: ${styling.inputFocusBorder};
    outline: ${styling.inputFocusOutline};
    box-shadow: ${styling.inputFocusBoxShadow};
  }`;

  // Select disabled state
  css += `#ccexpirymonth:disabled, #ccexpiryyear:disabled, select:disabled {
    background-color: #f3f4f6;
    border-color: #d1d5db;
    color: #9ca3af;
    cursor: not-allowed;
    opacity: 0.6;
  }`;

  // Label styling - targeting specific CardPointe labels
  css += `#cccardlabel, #ccexpirylabel, #cccvvlabel, label {
    color: ${styling.labelColor};
    font-size: ${styling.labelFontSize};
    font-weight: ${styling.labelFontWeight};
    margin-top: ${styling.labelMarginTop};
    margin-bottom: ${styling.labelMarginBottom};
    display: block;
    font-family: ${styling.inputFontFamily};
  }`;

  // Error styling - targeting CardPointe error class
  css += `.error, #ccnumfield.error, #cccvvfield.error {
    color: ${styling.errorColor};
    font-size: ${styling.errorFontSize};
    margin-top: ${styling.errorMarginTop};
    display: block;
    border-color: ${styling.errorColor} !important;
    box-shadow: 0 0 0 2px rgba(220, 38, 38, 0.1) !important;
  }`;

  // Layout styling - CardPointe form structure
  css += `.field {
    margin-bottom: ${styling.fieldMarginBottom};
  }`;

  // CardPointe specific form styling
  css += `#tokenform {
    font-family: ${styling.inputFontFamily};
    line-height: 1.5;
  }`;

  // Style the year select margin (CardPointe has inline style)
  css += `#ccexpiryyear {
    margin-left: 12px !important;
  }`;

  // Hide the auto-generated hidden text input
  css += `input[type="text"][style*="display: none"] {
    display: none !important;
  }`;

  // Remove CardPointe's <br> tags to control spacing through CSS
  css += `br {
    display: none !important;
  }`;

  css += `body {
    padding: ${styling.containerPadding};
    background-color: ${styling.containerBackground};
    margin: 0;
    font-family: ${styling.inputFontFamily};
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }`;

  // Additional catch-all selectors to ensure all inputs are styled
  css += `* {
    box-sizing: border-box;
  }`;

  // Target any element that might be used as input (fallback for CardPointe)
  css += `[type="tel"], [type="text"], [type="number"] {
    background-color: ${styling.inputBackground};
    border: ${styling.inputBorder};
    border-radius: ${styling.inputBorderRadius};
    padding: ${styling.inputPadding};
    font-size: ${styling.inputFontSize};
    font-family: ${styling.inputFontFamily};
    color: ${styling.inputTextColor};
    height: ${styling.inputHeight};
    transition: all 0.2s ease-in-out;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  }`;

  // Add custom CSS if provided
  if (customCss && customCss.trim()) {
    css += customCss;
  }

  return css;
};

// Computed property to generate iframe URL
const iframeUrl = computed(() => {
  const config = cardPointeConfig.value;
  const params = new URLSearchParams();

  // Generate and add CSS parameter
  const css = generateCss();
  if (css) {
    params.append("css", css);
  }

  // Add all non-empty configuration options to URL parameters
  Object.entries(config).forEach(([key, value]) => {
    if (key === "baseUrl" || key === "customCss" || key === "styling") return; // Skip these as they're handled separately

    if (value !== "" && value !== null && value !== undefined) {
      // Convert boolean values to string
      if (typeof value === "boolean") {
        params.append(key, value.toString());
      } else if (typeof value === "string" && value.trim() !== "") {
        params.append(key, value);
      } else if (typeof value === "number") {
        params.append(key, value.toString());
      }
    }
  });

  // Convert + signs to %20 for proper space encoding (CardPointe prefers %20 over +)
  const queryString = params.toString().replace(/\+/g, "%20");
  return queryString ? `${config.baseUrl}?${queryString}` : config.baseUrl;
});

// Event handlers
const onIframeLoad = () => {
  isLoading.value = false;
  console.log("CardPointe iframe loaded successfully");
};

const processPayment = async (event) => {
  if (!token.value) {
    error.value = "Please generate a token first";
    return;
  }

  isProcessing.value = true;
  error.value = "";

  try {
    // Get form data including the token and expiry from hidden inputs
    const formData = new FormData(event.target);
    const tokenFromForm = formData.get("mytoken");
    const expiryFromForm = formData.get("expiry");

    console.log("Form token:", tokenFromForm);
    console.log("Form expiry:", expiryFromForm);
    console.log("Reactive token:", token.value);
    console.log("Reactive expiry:", expiry.value);

    // Simulate payment processing
    await new Promise((resolve) => setTimeout(resolve, 2000));

    // In a real implementation, you would send the token to your backend
    // Example payload that would be sent to your server:
    const paymentData = {
      token: tokenFromForm || token.value,
      expiry: expiryFromForm || expiry.value,
      amount: 3269, // $32.69 in cents
      currency: "USD",
      // Add other payment details as needed
    };

    console.log("Payment data to be sent to backend:", paymentData);

    // Show success message
    alert(
      "Payment processed successfully! (Demo)\nCheck console for payment data"
    );
  } catch (err) {
    error.value = "Payment processing failed";
    console.error("Payment error:", err);
  } finally {
    isProcessing.value = false;
  }
};

// Message listener for iframe communication
const handleMessage = (event) => {
  // Ensure message is from CardPointe
  if (event.origin !== "https://boltgw-uat.cardconnect.com") {
    return;
  }

  console.log("handleMessage", event);

  try {
    // Parse the JSON string from the iframe
    const data =
      typeof event.data === "string" ? JSON.parse(event.data) : event.data;
    console.log("Parsed data:", data);

    // CardPointe sends the token in the configured token property field
    const tokenPropName = cardPointeConfig.value.tokenpropname;
    if (data[tokenPropName]) {
      token.value = data[tokenPropName];
      expiry.value = data.expiry || "";

      // Also populate the hidden input elements
      const tokenInput = document.getElementById("mytoken");
      if (tokenInput) {
        tokenInput.value = data[tokenPropName];
      }

      const expiryInput = document.getElementById("expiry");
      if (expiryInput && data.expiry) {
        expiryInput.value = data.expiry;
      }
      error.value = "";
      console.log("Token received:", data[tokenPropName]);
      console.log("Expiry received:", data.expiry);
    }

    if (data.error) {
      error.value = data.error;
      console.error("CardPointe error:", data.error);
    }

    // Handle validation errors
    if (data.validationError) {
      error.value = data.validationError;
      console.error("Validation error:", data.validationError);
    }

    // Handle card typing events
    if (data.cardTyping !== undefined) {
      console.log("Card typing:", data.cardTyping);
    }

    // Handle other events
    if (data.type === "cardtype") {
      console.log("Card type detected:", data.cardtype);
    }

    // Handle enhanced response fields (when enhancedresponse=true)
    if (data.errorCode !== undefined) {
      console.log("Error code:", data.errorCode);
    }
    if (data.errorMessage) {
      console.log("Error message:", data.errorMessage);
    }
  } catch (err) {
    console.error("Error handling message:", err);
  }
};

watch(token, (newVal) => {
  console.log("Token changed:", newVal);
});

watch(expiry, (newVal) => {
  console.log("Expiry changed:", newVal);
});

// Watch for iframe URL changes
watch(
  iframeUrl,
  (newVal) => {
    console.log("Generated iframe URL:", newVal);
  },
  { immediate: true }
);

// Lifecycle hooks
onMounted(() => {
  window.addEventListener("message", handleMessage);
});

onUnmounted(() => {
  window.removeEventListener("message", handleMessage);
});
</script>

<style scoped>
/* Additional custom styles if needed */
</style>
