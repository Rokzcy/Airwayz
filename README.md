<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rokzcy Airways - Fly Beyond Limits</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .hero-bg {
            background-image: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url('https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80');
            background-size: cover;
            background-position: center;
        }
        
        .flight-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .loading-spinner {
            border: 4px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 4px solid #3b82f6;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .seat {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 5px;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .seat:hover {
            transform: scale(1.1);
        }
        
        .seat.selected {
            background-color: #3b82f6;
            color: white;
        }
        
        .seat.booked {
            background-color: #6b7280;
            color: white;
            cursor: not-allowed;
        }
        
        .seat.available {
            background-color: #e5e7eb;
            color: black;
        }
    </style>
</head>
<body class="bg-gray-100 font-sans">
    <!-- Navigation -->
    <nav class="bg-blue-900 text-white shadow-lg">
        <div class="container mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <i class="fas fa-plane-departure text-2xl"></i>
                <a href="#" class="text-2xl font-bold">Rokzcy Airways</a>
            </div>
            <div class="hidden md:flex space-x-6">
                <a href="#flights" class="hover:text-blue-200 transition">Flights</a>
                <a href="#destinations" class="hover:text-blue-200 transition">Destinations</a>
                <a href="#offers" class="hover:text-blue-200 transition">Offers</a>
                <a href="#about" class="hover:text-blue-200 transition">About Us</a>
            </div>
            <div class="flex items-center space-x-4">
                <button id="loginBtn" class="bg-white text-blue-900 px-4 py-2 rounded-lg font-medium hover:bg-blue-100 transition">Login</button>
                <button id="signupBtn" class="bg-blue-600 text-white px-4 py-2 rounded-lg font-medium hover:bg-blue-700 transition">Sign Up</button>
                <button id="adminBtn" class="hidden bg-red-600 text-white px-4 py-2 rounded-lg font-medium hover:bg-red-700 transition">Admin</button>
                <button id="logoutBtn" class="hidden bg-gray-600 text-white px-4 py-2 rounded-lg font-medium hover:bg-gray-700 transition">Logout</button>
                <button id="mobileMenuBtn" class="md:hidden text-2xl">
                    <i class="fas fa-bars"></i>
                </button>
            </div>
        </div>
        <!-- Mobile Menu -->
        <div id="mobileMenu" class="hidden md:hidden bg-blue-800 px-4 py-2">
            <a href="#flights" class="block py-2 hover:text-blue-200 transition">Flights</a>
            <a href="#destinations" class="block py-2 hover:text-blue-200 transition">Destinations</a>
            <a href="#offers" class="block py-2 hover:text-blue-200 transition">Offers</a>
            <a href="#about" class="block py-2 hover:text-blue-200 transition">About Us</a>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero-bg text-white py-20">
        <div class="container mx-auto px-4 text-center">
            <h1 class="text-4xl md:text-6xl font-bold mb-6">Fly Beyond Limits</h1>
            <p class="text-xl md:text-2xl mb-8">Experience luxury in the skies with Rokzcy Airways</p>
            
            <!-- Flight Search Form -->
            <div class="max-w-4xl mx-auto bg-white rounded-lg shadow-xl p-6">
                <div class="flex flex-col md:flex-row gap-4">
                    <div class="flex-1">
                        <label class="block text-gray-700 font-medium mb-2">From</label>
                        <select id="fromCity" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-700">
                            <option value="">Select departure city</option>
                            <option value="JFK">New York (JFK)</option>
                            <option value="LAX">Los Angeles (LAX)</option>
                            <option value="ORD">Chicago (ORD)</option>
                            <option value="DFW">Dallas (DFW)</option>
                            <option value="MIA">Miami (MIA)</option>
                        </select>
                    </div>
                    <div class="flex-1">
                        <label class="block text-gray-700 font-medium mb-2">To</label>
                        <select id="toCity" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-700">
                            <option value="">Select arrival city</option>
                            <option value="LHR">London (LHR)</option>
                            <option value="CDG">Paris (CDG)</option>
                            <option value="DXB">Dubai (DXB)</option>
                            <option value="HND">Tokyo (HND)</option>
                            <option value="SYD">Sydney (SYD)</option>
                        </select>
                    </div>
                </div>
                <div class="flex flex-col md:flex-row gap-4 mt-4">
                    <div class="flex-1">
                        <label class="block text-gray-700 font-medium mb-2">Departure</label>
                        <input type="date" id="departureDate" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-700">
                    </div>
                    <div class="flex-1">
                        <label class="block text-gray-700 font-medium mb-2">Return (Optional)</label>
                        <input type="date" id="returnDate" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-700">
                    </div>
                    <div class="flex-1">
                        <label class="block text-gray-700 font-medium mb-2">Passengers</label>
                        <select id="passengers" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-700">
                            <option value="1">1 Passenger</option>
                            <option value="2">2 Passengers</option>
                            <option value="3">3 Passengers</option>
                            <option value="4">4 Passengers</option>
                            <option value="5">5 Passengers</option>
                        </select>
                    </div>
                </div>
                <button id="searchFlightsBtn" class="mt-6 w-full bg-blue-600 text-white py-3 px-6 rounded-lg font-medium hover:bg-blue-700 transition flex items-center justify-center">
                    <span>Search Flights</span>
                    <div id="searchLoading" class="loading-spinner ml-2 hidden"></div>
                </button>
            </div>
        </div>
    </section>

    <!-- Flight Results Section -->
    <section id="flights" class="py-16 bg-gray-100">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Available Flights</h2>
            
            <div id="flightResults" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Flight cards will be inserted here by JavaScript -->
                <div class="text-center py-10 text-gray-500">
                    <i class="fas fa-plane text-4xl mb-4"></i>
                    <p>Search for flights to see available options</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Popular Destinations -->
    <section id="destinations" class="py-16 bg-white">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Popular Destinations</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <div class="relative overflow-hidden rounded-xl shadow-lg h-64 group">
                    <img src="https://images.unsplash.com/photo-1502602898657-3e91760cbb34?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1473&q=80" alt="Paris" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent flex items-end p-6">
                        <div>
                            <h3 class="text-white text-xl font-bold">Paris</h3>
                            <p class="text-white/80">From $499</p>
                            <button class="mt-2 bg-blue-600 text-white px-4 py-2 rounded-lg opacity-0 group-hover:opacity-100 transition">Book Now</button>
                        </div>
                    </div>
                </div>
                
                <div class="relative overflow-hidden rounded-xl shadow-lg h-64 group">
                    <img src="https://images.unsplash.com/photo-1533929736458-ca588d08c8be?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80" alt="London" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent flex items-end p-6">
                        <div>
                            <h3 class="text-white text-xl font-bold">London</h3>
                            <p class="text-white/80">From $599</p>
                            <button class="mt-2 bg-blue-600 text-white px-4 py-2 rounded-lg opacity-0 group-hover:opacity-100 transition">Book Now</button>
                        </div>
                    </div>
                </div>
                
                <div class="relative overflow-hidden rounded-xl shadow-lg h-64 group">
                    <img src="https://images.unsplash.com/photo-1518684079-3c830dcef090?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80" alt="Tokyo" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent flex items-end p-6">
                        <div>
                            <h3 class="text-white text-xl font-bold">Tokyo</h3>
                            <p class="text-white/80">From $899</p>
                            <button class="mt-2 bg-blue-600 text-white px-4 py-2 rounded-lg opacity-0 group-hover:opacity-100 transition">Book Now</button>
                        </div>
                    </div>
                </div>
                
                <div class="relative overflow-hidden rounded-xl shadow-lg h-64 group">
                    <img src="https://images.unsplash.com/photo-1523482580672-f109ba8cb9be?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1530&q=80" alt="Dubai" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent flex items-end p-6">
                        <div>
                            <h3 class="text-white text-xl font-bold">Dubai</h3>
                            <p class="text-white/80">From $799</p>
                            <button class="mt-2 bg-blue-600 text-white px-4 py-2 rounded-lg opacity-0 group-hover:opacity-100 transition">Book Now</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Special Offers -->
    <section id="offers" class="py-16 bg-blue-50">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Special Offers</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="bg-white rounded-xl shadow-lg overflow-hidden">
                    <div class="md:flex">
                        <div class="md:w-1/3">
                            <img src="https://images.unsplash.com/photo-1551882547-ff40c63fe5fa?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80" alt="Summer Sale" class="w-full h-full object-cover">
                        </div>
                        <div class="p-6 md:w-2/3">
                            <div class="flex justify-between items-start">
                                <h3 class="text-xl font-bold text-gray-800">Summer Sale</h3>
                                <span class="bg-red-500 text-white text-xs font-bold px-2 py-1 rounded">30% OFF</span>
                            </div>
                            <p class="text-gray-600 mt-2">Book your summer getaway now and save up to 30% on selected flights!</p>
                            <div class="mt-4 flex items-center">
                                <span class="text-gray-500 line-through mr-2">$999</span>
                                <span class="text-blue-600 font-bold">$699</span>
                            </div>
                            <button class="mt-4 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition">Book Now</button>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-xl shadow-lg overflow-hidden">
                    <div class="md:flex">
                        <div class="md:w-1/3">
                            <img src="https://images.unsplash.com/photo-1506197603052-3cc9c3a201bd?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80" alt="Business Class" class="w-full h-full object-cover">
                        </div>
                        <div class="p-6 md:w-2/3">
                            <div class="flex justify-between items-start">
                                <h3 class="text-xl font-bold text-gray-800">Business Class Upgrade</h3>
                                <span class="bg-green-500 text-white text-xs font-bold px-2 py-1 rounded">UPGRADE</span>
                            </div>
                            <p class="text-gray-600 mt-2">Upgrade to Business Class for just $200 more and enjoy premium services!</p>
                            <div class="mt-4 flex items-center">
                                <span class="text-gray-500 mr-2">From Economy</span>
                                <span class="text-blue-600 font-bold">+$200</span>
                            </div>
                            <button class="mt-4 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition">Upgrade Now</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- About Us -->
    <section id="about" class="py-16 bg-gray-800 text-white">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12">About Rokzcy Airways</h2>
            
            <div class="max-w-4xl mx-auto">
                <p class="text-lg mb-6">
                    Founded in 2023, Rokzcy Airways is a premium airline dedicated to providing exceptional service and comfort to our passengers. 
                    With a modern fleet of aircraft and a team of highly trained professionals, we ensure your journey is as enjoyable as your destination.
                </p>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mt-10">
                    <div class="text-center">
                        <div class="bg-blue-600 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                            <i class="fas fa-shield-alt text-2xl"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Safety First</h3>
                        <p class="text-gray-300">Our top priority is your safety with industry-leading standards and protocols.</p>
                    </div>
                    
                    <div class="text-center">
                        <div class="bg-blue-600 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                            <i class="fas fa-heart text-2xl"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Customer Care</h3>
                        <p class="text-gray-300">24/7 support to ensure your travel experience is seamless and enjoyable.</p>
                    </div>
                    
                    <div class="text-center">
                        <div class="bg-blue-600 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                            <i class="fas fa-globe-americas text-2xl"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Global Network</h3>
                        <p class="text-gray-300">Connecting you to over 100 destinations across 6 continents.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-12">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <h3 class="text-xl font-bold mb-4 flex items-center">
                        <i class="fas fa-plane-departure mr-2"></i> Rokzcy Airways
                    </h3>
                    <p class="text-gray-400">Fly Beyond Limits with our premium services and exceptional customer care.</p>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">Quick Links</h4>
                    <ul class="space-y-2">
                        <li><a href="#" class="text-gray-400 hover:text-white transition">Home</a></li>
                        <li><a href="#flights" class="text-gray-400 hover:text-white transition">Flights</a></li>
                        <li><a href="#destinations" class="text-gray-400 hover:text-white transition">Destinations</a></li>
                        <li><a href="#offers" class="text-gray-400 hover:text-white transition">Offers</a></li>
                        <li><a href="#about" class="text-gray-400 hover:text-white transition">About Us</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">Contact Us</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li class="flex items-center">
                            <i class="fas fa-map-marker-alt mr-2"></i> 123 Aviation Way, New York, NY
                        </li>
                        <li class="flex items-center">
                            <i class="fas fa-phone mr-2"></i> +1 (800) 555-ROKZ
                        </li>
                        <li class="flex items-center">
                            <i class="fas fa-envelope mr-2"></i> contact@rokzcyairways.com
                        </li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">Follow Us</h4>
                    <div class="flex space-x-4">
                        <a href="#" class="bg-gray-700 w-10 h-10 rounded-full flex items-center justify-center hover:bg-blue-600 transition">
                            <i class="fab fa-facebook-f"></i>
                        </a>
                        <a href="#" class="bg-gray-700 w-10 h-10 rounded-full flex items-center justify-center hover:bg-blue-400 transition">
                            <i class="fab fa-twitter"></i>
                        </a>
                        <a href="#" class="bg-gray-700 w-10 h-10 rounded-full flex items-center justify-center hover:bg-pink-600 transition">
                            <i class="fab fa-instagram"></i>
                        </a>
                        <a href="#" class="bg-gray-700 w-10 h-10 rounded-full flex items-center justify-center hover:bg-red-600 transition">
                            <i class="fab fa-youtube"></i>
                        </a>
                    </div>
                    
                    <h4 class="text-lg font-bold mt-6 mb-2">Newsletter</h4>
                    <div class="flex">
                        <input type="email" placeholder="Your email" class="bg-gray-700 text-white px-4 py-2 rounded-l-lg focus:outline-none w-full">
                        <button class="bg-blue-600 px-4 py-2 rounded-r-lg hover:bg-blue-700 transition">
                            <i class="fas fa-paper-plane"></i>
                        </button>
                    </div>
                </div>
            </div>
            
            <div class="border-t border-gray-800 mt-10 pt-6 text-center text-gray-500">
                <p>&copy; 2023 Rokzcy Airways. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <!-- Modals -->
    <!-- Login Modal -->
    <div id="loginModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-md">
            <div class="p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-2xl font-bold text-gray-800">Login to Your Account</h3>
                    <button id="closeLoginModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <form id="loginForm">
                    <div class="mb-4">
                        <label class="block text-gray-700 font-medium mb-2">Email</label>
                        <input type="email" id="loginEmail" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    </div>
                    
                    <div class="mb-6">
                        <label class="block text-gray-700 font-medium mb-2">Password</label>
                        <input type="password" id="loginPassword" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    </div>
                    
                    <button type="submit" class="w-full bg-blue-600 text-white py-3 px-6 rounded-lg font-medium hover:bg-blue-700 transition flex items-center justify-center">
                        <span>Login</span>
                        <div id="loginLoading" class="loading-spinner ml-2 hidden"></div>
                    </button>
                </form>
                
                <div class="mt-4 text-center">
                    <p class="text-gray-600">Don't have an account? <button id="switchToSignup" class="text-blue-600 hover:underline">Sign up</button></p>
                </div>
            </div>
        </div>
    </div>

    <!-- Signup Modal -->
    <div id="signupModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-md">
            <div class="p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-2xl font-bold text-gray-800">Create Your Account</h3>
                    <button id="closeSignupModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <form id="signupForm">
                    <div class="mb-4">
                        <label class="block text-gray-700 font-medium mb-2">Full Name</label>
                        <input type="text" id="signupName" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    </div>
                    
                    <div class="mb-4">
                        <label class="block text-gray-700 font-medium mb-2">Email</label>
                        <input type="email" id="signupEmail" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    </div>
                    
                    <div class="mb-4">
                        <label class="block text-gray-700 font-medium mb-2">Password</label>
                        <input type="password" id="signupPassword" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    </div>
                    
                    <div class="mb-6">
                        <label class="block text-gray-700 font-medium mb-2">Confirm Password</label>
                        <input type="password" id="signupConfirmPassword" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    </div>
                    
                    <button type="submit" class="w-full bg-blue-600 text-white py-3 px-6 rounded-lg font-medium hover:bg-blue-700 transition flex items-center justify-center">
                        <span>Create Account</span>
                        <div id="signupLoading" class="loading-spinner ml-2 hidden"></div>
                    </button>
                </form>
                
                <div class="mt-4 text-center">
                    <p class="text-gray-600">Already have an account? <button id="switchToLogin" class="text-blue-600 hover:underline">Login</button></p>
                </div>
            </div>
        </div>
    </div>

    <!-- Flight Details Modal -->
    <div id="flightDetailsModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden overflow-y-auto">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-4xl max-h-screen overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-2xl font-bold text-gray-800">Flight Details</h3>
                    <button id="closeFlightDetailsModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <div id="flightDetailsContent">
                    <!-- Flight details will be inserted here by JavaScript -->
                </div>
            </div>
        </div>
    </div>

    <!-- Booking Modal -->
    <div id="bookingModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden overflow-y-auto">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-4xl max-h-screen overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-2xl font-bold text-gray-800">Complete Your Booking</h3>
                    <button id="closeBookingModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <div id="bookingContent">
                    <!-- Booking form will be inserted here by JavaScript -->
                </div>
            </div>
        </div>
    </div>

    <!-- Seat Selection Modal -->
    <div id="seatSelectionModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden overflow-y-auto">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-4xl max-h-screen overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-2xl font-bold text-gray-800">Select Your Seats</h3>
                    <button id="closeSeatSelectionModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <div id="seatSelectionContent">
                    <!-- Seat selection will be inserted here by JavaScript -->
                </div>
            </div>
        </div>
    </div>

    <!-- Payment Modal -->
    <div id="paymentModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-md">
            <div class="p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-2xl font-bold text-gray-800">Payment Information</h3>
                    <button id="closePaymentModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <div id="paymentContent">
                    <!-- Payment form will be inserted here by JavaScript -->
                </div>
            </div>
        </div>
    </div>

    <!-- Booking Confirmation Modal -->
    <div id="confirmationModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-md">
            <div class="p-6 text-center">
                <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                    <i class="fas fa-check text-green-600 text-2xl"></i>
                </div>
                
                <h3 class="text-2xl font-bold text-gray-800 mb-2">Booking Confirmed!</h3>
                <p class="text-gray-600 mb-6">Your flight has been successfully booked. A confirmation has been sent to your email.</p>
                
                <div id="bookingReference" class="bg-gray-100 p-4 rounded-lg mb-6">
                    <p class="font-medium">Booking Reference:</p>
                    <p class="text-blue-600 font-bold text-xl">ROKZC-<span id="referenceNumber">123456</span></p>
                </div>
                
                <button id="closeConfirmationModal" class="w-full bg-blue-600 text-white py-3 px-6 rounded-lg font-medium hover:bg-blue-700 transition">
                    Done
                </button>
            </div>
        </div>
    </div>

    <!-- Admin Panel Modal -->
    <div id="adminModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden overflow-y-auto">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-6xl max-h-screen overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-2xl font-bold text-gray-800">Admin Dashboard</h3>
                    <button id="closeAdminModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <div class="mb-6">
                    <div class="flex space-x-4 mb-4">
                        <button id="adminFlightsTab" class="px-4 py-2 bg-blue-600 text-white rounded-lg font-medium">Flights</button>
                        <button id="adminBookingsTab" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-lg font-medium">Bookings</button>
                        <button id="adminUsersTab" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-lg font-medium">Users</button>
                    </div>
                    
                    <div id="adminFlightsContent">
                        <div class="flex justify-between items-center mb-4">
                            <h4 class="text-xl font-bold">Manage Flights</h4>
                            <button id="addFlightBtn" class="bg-green-600 text-white px-4 py-2 rounded-lg hover:bg-green-700 transition">
                                <i class="fas fa-plus mr-2"></i> Add Flight
                            </button>
                        </div>
                        
                        <div class="overflow-x-auto">
                            <table class="min-w-full bg-white">
                                <thead>
                                    <tr class="bg-gray-100">
                                        <th class="py-3 px-4 text-left">Flight #</th>
                                        <th class="py-3 px-4 text-left">Route</th>
                                        <th class="py-3 px-4 text-left">Departure</th>
                                        <th class="py-3 px-4 text-left">Arrival</th>
                                        <th class="py-3 px-4 text-left">Price</th>
                                        <th class="py-3 px-4 text-left">Seats</th>
                                        <th class="py-3 px-4 text-left">Actions</th>
                                    </tr>
                                </thead>
                                <tbody id="adminFlightsTable">
                                    <!-- Flights will be inserted here by JavaScript -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                    
                    <div id="adminBookingsContent" class="hidden">
                        <h4 class="text-xl font-bold mb-4">Manage Bookings</h4>
                        <div class="overflow-x-auto">
                            <table class="min-w-full bg-white">
                                <thead>
                                    <tr class="bg-gray-100">
                                        <th class="py-3 px-4 text-left">Booking #</th>
                                        <th class="py-3 px-4 text-left">Flight</th>
                                        <th class="py-3 px-4 text-left">Passenger</th>
                                        <th class="py-3 px-4 text-left">Date</th>
                                        <th class="py-3 px-4 text-left">Seats</th>
                                        <th class="py-3 px-4 text-left">Total</th>
                                        <th class="py-3 px-4 text-left">Status</th>
                                        <th class="py-3 px-4 text-left">Actions</th>
                                    </tr>
                                </thead>
                                <tbody id="adminBookingsTable">
                                    <!-- Bookings will be inserted here by JavaScript -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                    
                    <div id="adminUsersContent" class="hidden">
                        <h4 class="text-xl font-bold mb-4">Manage Users</h4>
                        <div class="overflow-x-auto">
                            <table class="min-w-full bg-white">
                                <thead>
                                    <tr class="bg-gray-100">
                                        <th class="py-3 px-4 text-left">Name</th>
                                        <th class="py-3 px-4 text-left">Email</th>
                                        <th class="py-3 px-4 text-left">Role</th>
                                        <th class="py-3 px-4 text-left">Bookings</th>
                                        <th class="py-3 px-4 text-left">Actions</th>
                                    </tr>
                                </thead>
                                <tbody id="adminUsersTable">
                                    <!-- Users will be inserted here by JavaScript -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Add/Edit Flight Modal -->
    <div id="flightFormModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-2xl">
            <div class="p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-2xl font-bold text-gray-800" id="flightFormTitle">Add New Flight</h3>
                    <button id="closeFlightFormModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                
                <form id="flightForm">
                    <input type="hidden" id="flightId">
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Flight Number</label>
                            <input type="text" id="flightNumber" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Aircraft Type</label>
                            <select id="aircraftType" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                                <option value="Boeing 737">Boeing 737</option>
                                <option value="Boeing 787">Boeing 787</option>
                                <option value="Airbus A320">Airbus A320</option>
                                <option value="Airbus A350">Airbus A350</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Departure Airport</label>
                            <select id="departureAirport" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                                <option value="JFK">New York (JFK)</option>
                                <option value="LAX">Los Angeles (LAX)</option>
                                <option value="ORD">Chicago (ORD)</option>
                                <option value="DFW">Dallas (DFW)</option>
                                <option value="MIA">Miami (MIA)</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Arrival Airport</label>
                            <select id="arrivalAirport" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                                <option value="LHR">London (LHR)</option>
                                <option value="CDG">Paris (CDG)</option>
                                <option value="DXB">Dubai (DXB)</option>
                                <option value="HND">Tokyo (HND)</option>
                                <option value="SYD">Sydney (SYD)</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Departure Date & Time</label>
                            <input type="datetime-local" id="departureDateTime" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Arrival Date & Time</label>
                            <input type="datetime-local" id="arrivalDateTime" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Economy Price ($)</label>
                            <input type="number" id="economyPrice" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Business Price ($)</label>
                            <input type="number" id="businessPrice" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Total Seats</label>
                            <input type="number" id="totalSeats" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Available Seats</label>
                            <input type="number" id="availableSeats" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                    </div>
                    
                    <div class="mt-6">
                        <button type="submit" class="w-full bg-blue-600 text-white py-3 px-6 rounded-lg font-medium hover:bg-blue-700 transition flex items-center justify-center">
                            <span id="flightFormSubmitText">Add Flight</span>
                            <div id="flightFormLoading" class="loading-spinner ml-2 hidden"></div>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- JavaScript -->
    <script>
        // Database simulation (in a real app, this would be server-side)
        const database = {
            users: [
                { id: 1, name: "Admin User", email: "admin@rokzcy.com", password: "admin123", role: "admin" },
                { id: 2, name: "John Doe", email: "john@example.com", password: "password123", role: "user" }
            ],
            flights: [
                { 
                    id: 1, 
                    flightNumber: "ROK101", 
                    aircraftType: "Boeing 787", 
                    departureAirport: "JFK", 
                    arrivalAirport: "LHR", 
                    departureDateTime: "2023-12-15T08:00:00", 
                    arrivalDateTime: "2023-12-15T20:00:00", 
                    economyPrice: 499, 
                    businessPrice: 1299, 
                    totalSeats: 200, 
                    availableSeats: 150,
                    status: "scheduled"
                },
                { 
                    id: 2, 
                    flightNumber: "ROK202", 
                    aircraftType: "Airbus A350", 
                    departureAirport: "LAX", 
                    arrivalAirport: "SYD", 
                    departureDateTime: "2023-12-16T10:00:00", 
                    arrivalDateTime: "2023-12-17T06:00:00", 
                    economyPrice: 899, 
                    businessPrice: 1999, 
                    totalSeats: 250, 
                    availableSeats: 200,
                    status: "scheduled"
                }
            ],
            bookings: [
                { 
                    id: 1, 
                    reference: "ROKZC-100001", 
                    flightId: 1, 
                    userId: 2, 
                    passengerName: "John Doe", 
                    passengerEmail: "john@example.com", 
                    seats: ["12A", "12B"], 
                    class: "economy", 
                    totalPrice: 998, 
                    bookingDate: "2023-11-01T14:30:00",
                    status: "confirmed"
                }
            ],
            nextUserId: 3,
            nextFlightId: 3,
            nextBookingId: 2
        };

        // Current user state
        let currentUser = null;
        let selectedFlight = null;
        let selectedSeats = [];
        let bookingDetails = {};

        // DOM Elements
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');
        const mobileMenu = document.getElementById('mobileMenu');
        const loginBtn = document.getElementById('loginBtn');
        const signupBtn = document.getElementById('signupBtn');
        const adminBtn = document.getElementById('adminBtn');
        const logoutBtn = document.getElementById('logoutBtn');
        const loginModal = document.getElementById('loginModal');
        const signupModal = document.getElementById('signupModal');
        const closeLoginModal = document.getElementById('closeLoginModal');
        const closeSignupModal = document.getElementById('closeSignupModal');
        const switchToSignup = document.getElementById('switchToSignup');
        const switchToLogin = document.getElementById('switchToLogin');
        const loginForm = document.getElementById('loginForm');
        const signupForm = document.getElementById('signupForm');
        const searchFlightsBtn = document.getElementById('searchFlightsBtn');
        const flightResults = document.getElementById('flightResults');
        const flightDetailsModal = document.getElementById('flightDetailsModal');
        const closeFlightDetailsModal = document.getElementById('closeFlightDetailsModal');
        const flightDetailsContent = document.getElementById('flightDetailsContent');
        const bookingModal = document.getElementById('bookingModal');
        const closeBookingModal = document.getElementById('closeBookingModal');
        const bookingContent = document.getElementById('bookingContent');
        const seatSelectionModal = document.getElementById('seatSelectionModal');
        const closeSeatSelectionModal = document.getElementById('closeSeatSelectionModal');
        const seatSelectionContent = document.getElementById('seatSelectionContent');
        const paymentModal = document.getElementById('paymentModal');
        const closePaymentModal = document.getElementById('closePaymentModal');
        const paymentContent = document.getElementById('paymentContent');
        const confirmationModal = document.getElementById('confirmationModal');
        const closeConfirmationModal = document.getElementById('closeConfirmationModal');
        const adminModal = document.getElementById('adminModal');
        const closeAdminModal = document.getElementById('closeAdminModal');
        const adminFlightsTab = document.getElementById('adminFlightsTab');
        const adminBookingsTab = document.getElementById('adminBookingsTab');
        const adminUsersTab = document.getElementById('adminUsersTab');
        const adminFlightsContent = document.getElementById('adminFlightsContent');
        const adminBookingsContent = document.getElementById('adminBookingsContent');
        const adminUsersContent = document.getElementById('adminUsersContent');
        const adminFlightsTable = document.getElementById('adminFlightsTable');
        const adminBookingsTable = document.getElementById('adminBookingsTable');
        const adminUsersTable = document.getElementById('adminUsersTable');
        const addFlightBtn = document.getElementById('addFlightBtn');
        const flightFormModal = document.getElementById('flightFormModal');
        const closeFlightFormModal = document.getElementById('closeFlightFormModal');
        const flightForm = document.getElementById('flightForm');
        const flightFormTitle = document.getElementById('flightFormTitle');
        const flightFormSubmitText = document.getElementById('flightFormSubmitText');

        // Event Listeners
        mobileMenuBtn.addEventListener('click', toggleMobileMenu);
        loginBtn.addEventListener('click', () => showModal(loginModal));
        signupBtn.addEventListener('click', () => showModal(signupModal));
        adminBtn.addEventListener('click', () => {
            showModal(adminModal);
            loadAdminFlights();
        });
        logoutBtn.addEventListener('click', logout);
        closeLoginModal.addEventListener('click', () => hideModal(loginModal));
        closeSignupModal.addEventListener('click', () => hideModal(signupModal));
        switchToSignup.addEventListener('click', () => {
            hideModal(loginModal);
            showModal(signupModal);
        });
        switchToLogin.addEventListener('click', () => {
            hideModal(signupModal);
            showModal(loginModal);
        });
        loginForm.addEventListener('submit', handleLogin);
        signupForm.addEventListener('submit', handleSignup);
        searchFlightsBtn.addEventListener('click', searchFlights);
        closeFlightDetailsModal.addEventListener('click', () => hideModal(flightDetailsModal));
        closeBookingModal.addEventListener('click', () => hideModal(bookingModal));
        closeSeatSelectionModal.addEventListener('click', () => hideModal(seatSelectionModal));
        closePaymentModal.addEventListener('click', () => hideModal(paymentModal));
        closeConfirmationModal.addEventListener('click', () => hideModal(confirmationModal));
        closeAdminModal.addEventListener('click', () => hideModal(adminModal));
        adminFlightsTab.addEventListener('click', () => switchAdminTab('flights'));
        adminBookingsTab.addEventListener('click', () => switchAdminTab('bookings'));
        adminUsersTab.addEventListener('click', () => switchAdminTab('users'));
        addFlightBtn.addEventListener('click', () => {
            flightForm.reset();
            flightFormTitle.textContent = 'Add New Flight';
            flightFormSubmitText.textContent = 'Add Flight';
            document.getElementById('flightId').value = '';
            showModal(flightFormModal);
        });
        closeFlightFormModal.addEventListener('click', () => hideModal(flightFormModal));
        flightForm.addEventListener('submit', handleFlightFormSubmit);

        // Initialize the app
        function init() {
            // Check if user is logged in (in a real app, this would check session)
            updateUI();
        }

        // Toggle mobile menu
        function toggleMobileMenu() {
            mobileMenu.classList.toggle('hidden');
        }

        // Show modal
        function showModal(modal) {
            modal.classList.remove('hidden');
            document.body.style.overflow = 'hidden';
        }

        // Hide modal
        function hideModal(modal) {
            modal.classList.add('hidden');
            document.body.style.overflow = 'auto';
        }

        // Update UI based on user state
        function updateUI() {
            if (currentUser) {
                loginBtn.classList.add('hidden');
                signupBtn.classList.add('hidden');
                logoutBtn.classList.remove('hidden');
                
                if (currentUser.role === 'admin') {
                    adminBtn.classList.remove('hidden');
                } else {
                    adminBtn.classList.add('hidden');
                }
            } else {
                loginBtn.classList.remove('hidden');
                signupBtn.classList.remove('hidden');
                logoutBtn.classList.add('hidden');
                adminBtn.classList.add('hidden');
            }
        }

        // Handle login
        function handleLogin(e) {
            e.preventDefault();
            
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            const loginLoading = document.getElementById('loginLoading');
            loginLoading.classList.remove('hidden');
            
            // Simulate API call delay
            setTimeout(() => {
                const user = database.users.find(u => u.email === email && u.password === password);
                
                if (user) {
                    currentUser = user;
                    updateUI();
                    hideModal(loginModal);
                    showToast('Login successful!', 'success');
                } else {
                    showToast('Invalid email or password', 'error');
                }
                
                loginLoading.classList.add('hidden');
            }, 1000);
        }

        // Handle signup
        function handleSignup(e) {
            e.preventDefault();
            
            const name = document.getElementById('signupName').value;
            const email = document.getElementById('signupEmail').value;
            const password = document.getElementById('signupPassword').value;
            const confirmPassword = document.getElementById('signupConfirmPassword').value;
            
            if (password !== confirmPassword) {
                showToast('Passwords do not match', 'error');
                return;
            }
            
            const signupLoading = document.getElementById('signupLoading');
            signupLoading.classList.remove('hidden');
            
            // Simulate API call delay
            setTimeout(() => {
                const emailExists = database.users.some(u => u.email === email);
                
                if (emailExists) {
                    showToast('Email already in use', 'error');
                } else {
                    const newUser = {
                        id: database.nextUserId++,
                        name,
                        email,
                        password,
                        role: 'user'
                    };
                    
                    database.users.push(newUser);
                    currentUser = newUser;
                    updateUI();
                    hideModal(signupModal);
                    showToast('Account created successfully!', 'success');
                }
                
                signupLoading.classList.add('hidden');
            }, 1000);
        }

        // Handle logout
        function logout() {
            currentUser = null;
            updateUI();
            showToast('Logged out successfully', 'success');
        }

        // Search flights
        function searchFlights() {
            const fromCity = document.getElementById('fromCity').value;
            const toCity = document.getElementById('toCity').value;
            const departureDate = document.getElementById('departureDate').value;
            const returnDate = document.getElementById('returnDate').value;
            const passengers = document.getElementById('passengers').value;
            
            if (!fromCity || !toCity || !departureDate) {
                showToast('Please fill in all required fields', 'error');
                return;
            }
            
            const searchLoading = document.getElementById('searchLoading');
            searchLoading.classList.remove('hidden');
            
            // Simulate API call delay
            setTimeout(() => {
                // Filter flights based on search criteria
                const filteredFlights = database.flights.filter(flight => {
                    const flightDepartureDate = new Date(flight.departureDateTime).toISOString().split('T')[0];
                    return flight.departureAirport === fromCity && 
                           flight.arrivalAirport === toCity && 
                           flightDepartureDate === departureDate;
                });
                
                displayFlightResults(filteredFlights);
                searchLoading.classList.add('hidden');
            }, 1000);
        }

        // Display flight results
        function displayFlightResults(flights) {
            if (flights.length === 0) {
                flightResults.innerHTML = `
                    <div class="text-center py-10 text-gray-500 col-span-3">
                        <i class="fas fa-plane-slash text-4xl mb-4"></i>
                        <p>No flights found matching your criteria</p>
                    </div>
                `;
                return;
            }
            
            flightResults.innerHTML = flights.map(flight => `
                <div class="flight-card bg-white rounded-xl shadow-lg overflow-hidden transition duration-300">
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-4">
                            <div>
                                <h3 class="text-xl font-bold text-gray-800">${flight.flightNumber}</h3>
                                <p class="text-gray-600">${flight.aircraftType}</p>
                            </div>
                            <span class="bg-green-100 text-green-800 text-xs font-medium px-2.5 py-0.5 rounded">${flight.status}</span>
                        </div>
                        
                        <div class="flex justify-between items-center mb-4">
                            <div>
                                <p class="text-gray-800 font-medium">${formatTime(flight.departureDateTime)}</p>
                                <p class="text-gray-600 text-sm">${flight.departureAirport}</p>
                            </div>
                            <div class="text-center px-4">
                                <p class="text-gray-500 text-sm">${calculateFlightDuration(flight.departureDateTime, flight.arrivalDateTime)}</p>
                                <div class="relative mt-2">
                                    <div class="h-px bg-gray-300 w-full"></div>
                                    <div class="absolute -top-1.5 left-0 w-3 h-3 rounded-full bg-gray-300"></div>
                                    <div class="absolute -top-1.5 right-0 w-3 h-3 rounded-full bg-gray-300"></div>
                                    <i class="fas fa-plane absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-gray-400"></i>
                                </div>
                            </div>
                            <div class="text-right">
                                <p class="text-gray-800 font-medium">${formatTime(flight.arrivalDateTime)}</p>
                                <p class="text-gray-600 text-sm">${flight.arrivalAirport}</p>
                            </div>
                        </div>
                        
                        <div class="flex justify-between items-center mt-6">
                            <div>
                                <p class="text-gray-600">From</p>
                                <p class="text-xl font-bold text-blue-600">$${flight.economyPrice}</p>
                            </div>
                            <button class="view-details-btn bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition" data-flight-id="${flight.id}">
                                View Details
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
            
            // Add event listeners to view details buttons
            document.querySelectorAll('.view-details-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const flightId = parseInt(e.target.getAttribute('data-flight-id'));
                    selectedFlight = database.flights.find(f => f.id === flightId);
                    showFlightDetails(selectedFlight);
                });
            });
        }

        // Show flight details
        function showFlightDetails(flight) {
            flightDetailsContent.innerHTML = `
                <div class="mb-6">
                    <div class="flex justify-between items-start mb-4">
                        <div>
                            <h4 class="text-xl font-bold text-gray-800">${flight.flightNumber}</h4>
                            <p class="text-gray-600">${flight.aircraftType}</p>
                        </div>
                        <span class="bg-green-100 text-green-800 text-xs font-medium px-2.5 py-0.5 rounded">${flight.status}</span>
                    </div>
                    
                    <div class="bg-gray-100 p-4 rounded-lg mb-4">
                        <div class="flex justify-between items-center">
                            <div>
                                <p class="text-gray-800 font-medium">${formatDate(flight.departureDateTime)}</p>
                                <p class="text-gray-600 text-sm">${flight.departureAirport}</p>
                                <p class="text-gray-800 font-medium mt-2">${formatTime(flight.departureDateTime)}</p>
                            </div>
                            <div class="text-center px-4">
                                <p class="text-gray-500 text-sm">${calculateFlightDuration(flight.departureDateTime, flight.arrivalDateTime)}</p>
                                <div class="relative mt-2">
                                    <div class="h-px bg-gray-300 w-full"></div>
                                    <div class="absolute -top-1.5 left-0 w-3 h-3 rounded-full bg-gray-300"></div>
                                    <div class="absolute -top-1.5 right-0 w-3 h-3 rounded-full bg-gray-300"></div>
                                    <i class="fas fa-plane absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-gray-400"></i>
                                </div>
                            </div>
                            <div class="text-right">
                                <p class="text-gray-800 font-medium">${formatDate(flight.arrivalDateTime)}</p>
                                <p class="text-gray-600 text-sm">${flight.arrivalAirport}</p>
                                <p class="text-gray-800 font-medium mt-2">${formatTime(flight.arrivalDateTime)}</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                        <div class="bg-blue-50 p-4 rounded-lg">
                            <h5 class="font-bold text-gray-800 mb-2">Economy Class</h5>
                            <p class="text-gray-600 mb-2">From</p>
                            <p class="text-2xl font-bold text-blue-600">$${flight.economyPrice}</p>
                            <p class="text-gray-600 text-sm mt-2">${flight.availableSeats} seats available</p>
                        </div>
                        <div class="bg-blue-100 p-4 rounded-lg">
                            <h5 class="font-bold text-gray-800 mb-2">Business Class</h5>
                            <p class="text-gray-600 mb-2">From</p>
                            <p class="text-2xl font-bold text-blue-600">$${flight.businessPrice}</p>
                            <p class="text-gray-600 text-sm mt-2">${Math.floor(flight.availableSeats / 2)} seats available</p>
                        </div>
                    </div>
                </div>
                
                <div class="flex justify-end">
                    <button id="bookFlightBtn" class="bg-blue-600 text-white px-6 py-3 rounded-lg font-medium hover:bg-blue-700 transition">
                        Book Now
                    </button>
                </div>
            `;
            
            document.getElementById('bookFlightBtn').addEventListener('click', () => {
                if (!currentUser) {
                    showToast('Please login to book a flight', 'error');
                    showModal(loginModal);
                    hideModal(flightDetailsModal);
                    return;
                }
                
                showBookingForm();
            });
            
            showModal(flightDetailsModal);
        }

        // Show booking form
        function showBookingForm() {
            hideModal(flightDetailsModal);
            
            bookingContent.innerHTML = `
                <div class="mb-6">
                    <h4 class="text-xl font-bold text-gray-800 mb-4">Flight Details</h4>
                    <div class="bg-gray-100 p-4 rounded-lg">
                        <div class="flex justify-between items-center mb-2">
                            <div>
                                <p class="text-gray-800 font-medium">${selectedFlight.flightNumber}</p>
                                <p class="text-gray-600 text-sm">${selectedFlight.aircraftType}</p>
                            </div>
                            <span class="bg-green-100 text-green-800 text-xs font-medium px-2.5 py-0.5 rounded">${selectedFlight.status}</span>
                        </div>
                        
                        <div class="flex justify-between items-center mt-4">
                            <div>
                                <p class="text-gray-800 font-medium">${formatDate(selectedFlight.departureDateTime)}</p>
                                <p class="text-gray-600 text-sm">${selectedFlight.departureAirport}</p>
                                <p class="text-gray-800 font-medium mt-2">${formatTime(selectedFlight.departureDateTime)}</p>
                            </div>
                            <div class="text-center px-4">
                                <p class="text-gray-500 text-sm">${calculateFlightDuration(selectedFlight.departureDateTime, selectedFlight.arrivalDateTime)}</p>
                                <div class="relative mt-2">
                                    <div class="h-px bg-gray-300 w-full"></div>
                                    <div class="absolute -top-1.5 left-0 w-3 h-3 rounded-full bg-gray-300"></div>
                                    <div class="absolute -top-1.5 right-0 w-3 h-3 rounded-full bg-gray-300"></div>
                                    <i class="fas fa-plane absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-gray-400"></i>
                                </div>
                            </div>
                            <div class="text-right">
                                <p class="text-gray-800 font-medium">${formatDate(selectedFlight.arrivalDateTime)}</p>
                                <p class="text-gray-600 text-sm">${selectedFlight.arrivalAirport}</p>
                                <p class="text-gray-800 font-medium mt-2">${formatTime(selectedFlight.arrivalDateTime)}</p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <form id="passengerDetailsForm">
                    <h4 class="text-xl font-bold text-gray-800 mb-4">Passenger Details</h4>
                    
                    <div class="mb-4">
                        <label class="block text-gray-700 font-medium mb-2">Full Name</label>
                        <input type="text" id="passengerName" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" value="${currentUser ? currentUser.name : ''}" required>
                    </div>
                    
                    <div class="mb-4">
                        <label class="block text-gray-700 font-medium mb-2">Email</label>
                        <input type="email" id="passengerEmail" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" value="${currentUser ? currentUser.email : ''}" required>
                    </div>
                    
                    <div class="mb-4">
                        <label class="block text-gray-700 font-medium mb-2">Phone Number</label>
                        <input type="tel" id="passengerPhone" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    </div>
                    
                    <div class="mb-6">
                        <label class="block text-gray-700 font-medium mb-2">Class</label>
                        <select id="flightClass" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                            <option value="economy">Economy Class ($${selectedFlight.economyPrice})</option>
                            <option value="business">Business Class ($${selectedFlight.businessPrice})</option>
                        </select>
                    </div>
                    
                    <div class="flex justify-between">
                        <button type="button" id="backToFlightDetails" class="bg-gray-300 text-gray-800 px-6 py-3 rounded-lg font-medium hover:bg-gray-400 transition">
                            Back
                        </button>
                        <button type="submit" class="bg-blue-600 text-white px-6 py-3 rounded-lg font
</html>
