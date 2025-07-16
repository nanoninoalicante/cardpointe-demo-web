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
              <span>{{ showConfig ? 'Hide' : 'Show' }} Config</span>
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

            <!-- URL Preview -->
            <div class="border-t pt-6">
              <h4 class="font-medium text-gray-900 mb-3">Generated URL Preview</h4>
              <div class="bg-gray-50 p-4 rounded-lg">
                <code class="text-sm text-gray-800 break-all">{{ iframeUrl }}</code>
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
          <form @submit.prevent="processPayment" class="space-y-6" name="tokenform" id="tokenform">
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
                  height="400"
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

// CardPointe iframe configuration
const cardPointeConfig = ref({
  // Base URL for the iframe tokenizer
  baseUrl: "https://fts-uat.cardconnect.com/itoke/ajax-tokenizer.html",
  
  // Basic options
  useexpiry: true,                    // Collect expiration date
  usecvv: true,                       // Collect CVV/CVC
  
  // Focus and Input Controls
  autofocus: true,                   // If true, the input field will be focused when the page loads
  cardinputmaxlength: 2000,          // Controls the maximum character limit for the card number field
  cardnumbernumericonly: false,      // If true, the card number input field ignores non-numeric values
  
  // Input Formatting
  formatinput: false,                // Styles card number to be separated every four numbers
  maskfirsttwo: false,               // If true, the first 2 digits of the card number are masked
  
  // Input Labels
  cardlabel: "Card Number",          // Controls the text inside the label for the card number field
  cardtitle: "Credit Card Number",   // Controls the title and aria-label HTML attributes for card number input
  cvvlabel: "CVV",                   // Controls the text inside the label for the CVV field
  cvvtitle: "Card Verification Value", // Controls the title and aria-label HTML attributes for CVV input
  expirylabel: "Expiration Date",    // Controls the text inside the label for the expiration date selectors
  expirymonthtitle: "Expiration Month", // Controls the title and aria-label HTML attributes for expiry month
  expiryyeartitle: "Expiration Year",   // Controls the title and aria-label HTML attributes for expiry year
  
  // Response Options
  enhancedresponse: false,           // If true, includes additional parameters in JSON response (token, errorCode, errorMessage)
  
  // Mobile Options
  fullmobilekeyboard: false,         // Displays full alphanumeric keyboard in mobile browsers (for ACH input)
  
  // Timing Controls
  inactivityto: 500,                 // How long (ms) to wait after onInput event before considering input complete
  selectinputdelay: 0,               // Delay (ms) to ignore input to newly selected field (iOS fix)
  
  // Event Options
  sendcardtypingevent: true,         // Send event when user begins entering card number
  invalidcreditcardevent: false,     // Send event when card number is invalid (use instead of invalidinputevent with usecvv/useexpiry)
  invalidcvvevent: false,            // Send event when CVV is invalid (requires usecvv=true)
  invalidexpiryevent: false,         // Send event when expiry is invalid (requires useexpiry=true)
  invalidinputevent: false,          // Send event when card number is invalid (use when only card number required)
  
  // Layout Options
  orientation: "default",            // Controls orientation: default, horizontal, vertical, custom
  
  // Swipe Device Options
  swipeonly: false,                  // If true, only swipe input allowed (clears manual input)
  swiperate: 0.2,                    // Threshold for determining swipe vs typing (characters per ms)
  
  // Mobile Tokenization
  tokenizewheninactive: false,       // Perform tokenization when input stops (for mobile)
  
  // Token Options
  tokenpropname: "message",          // Name of token property in JSON message
  unique: false,                     // If true, generates unique token for each tokenization
});

// Computed property to generate iframe URL
const iframeUrl = computed(() => {
  const config = cardPointeConfig.value;
  const params = new URLSearchParams();
  
  // Add all non-empty configuration options to URL parameters
  Object.entries(config).forEach(([key, value]) => {
    if (key === 'baseUrl') return; // Skip baseUrl as it's not a parameter
    
    if (value !== "" && value !== null && value !== undefined) {
      // Convert boolean values to string
      if (typeof value === 'boolean') {
        params.append(key, value.toString());
      } else if (typeof value === 'string' && value.trim() !== '') {
        params.append(key, value);
      } else if (typeof value === 'number') {
        params.append(key, value.toString());
      }
    }
  });
  
  const queryString = params.toString();
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
    console.log("handleMessage", event);
    // Ensure message is from CardPointe
    if (event.origin !== "https://fts-uat.cardconnect.com") {
      return;
    }
  
    try {
      // Parse the JSON string from the iframe
      const data = typeof event.data === 'string' ? JSON.parse(event.data) : event.data;
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
  watch(iframeUrl, (newVal) => {
    console.log("Generated iframe URL:", newVal);
  }, { immediate: true });

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
