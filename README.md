# Powerplus-Gym-

npm create vite@latest powerplus-gym -- --template react
cd powerplus-gym
npm install
npm install lucide-react
npm install tailwindcss @tailwindcss/vite
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
@import "tailwindcss";

* {
  box-sizing: border-box;
  scroll-behavior: smooth;
}

body {
  margin: 0;
  background: #090b10;
  color: white;
  font-family: Arial, sans-serif;
}

::selection {
  background: #dfff00;
  color: black;
}

button {
  cursor: pointer;
}

.neon {
  color: #dfff00;
}

.neon-bg {
  background: #dfff00;
  color: #090b10;
}

.hero-bg {
  background:
    linear-gradient(90deg, rgba(5,7,12,.96), rgba(5,7,12,.55)),
    url("https://images.unsplash.com/photo-1534438327276-14e5300c3a48?w=1800")
    center/cover;
}

.glass {
  background: rgba(255,255,255,.045);
  border: 1px solid rgba(255,255,255,.10);
  backdrop-filter: blur(12px);
}

.card-hover {
  transition: .3s ease;
}

.card-hover:hover {
  transform: translateY(-8px);
  border-color: #dfff00;
}

input, select {
  color-scheme: dark;
}

input:focus, select:focus {
  outline: 1px solid #dfff00;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-12px); }
}

.float {
  animation: float 3s ease-in-out infinite;
}
import React, { useState } from "react";
import {
  Dumbbell, Zap, Menu, X, ArrowRight, Check,
  Activity, Target, Clock, Users, ShieldCheck,
  CreditCard, Smartphone, Wallet, ChevronRight
} from "lucide-react";

const plans = [
  {
    name: "Monthly Pass",
    price: 1500,
    duration: "1 Month",
    description: "Perfect for starting your fitness journey.",
    benefits: [
      "Unlimited Equipment Access",
      "Locker Room Access",
      "General Trainer Support",
      "Basic Workout Guidance"
    ]
  },
  {
    name: "Quarterly Power",
    price: 3999,
    duration: "3 Months",
    popular: true,
    description: "More consistency. More power. More savings.",
    benefits: [
      "Unlimited Equipment Access",
      "Locker Room Access",
      "Expert Trainer Support",
      "Diet Guidance",
      "Fitness Progress Tracking"
    ]
  },
  {
    name: "Annual Elite",
    price: 12999,
    duration: "12 Months",
    description: "The ultimate premium fitness experience.",
    benefits: [
      "All Quarterly Benefits",
      "Personal Training Sessions",
      "Personalized Diet Plan",
      "Priority Gym Access",
      "Monthly Body Analysis"
    ]
  }
];

const trainers = [
  {
    name: "Alex Morgan",
    role: "Strength Coach",
    exp: "8+ Years Experience",
    image: "https://images.unsplash.com/photo-1583454110551-21f2fa2afe61?w=500"
  },
  {
    name: "Sarah Williams",
    role: "Fitness & Nutrition",
    exp: "6+ Years Experience",
    image: "https://images.unsplash.com/photo-1544005313-94ddf0286df2?w=500"
  },
  {
    name: "David Smith",
    role: "Bodybuilding Coach",
    exp: "10+ Years Experience",
    image: "https://images.unsplash.com/photo-1567013127542-490d757e51fc?w=500"
  }
];

export default function App() {
  const [mobileMenu, setMobileMenu] = useState(false);
  const [result, setResult] = useState(null);
  const [selectedPlan, setSelectedPlan] = useState(null);
  const [paymentMethod, setPaymentMethod] = useState("UPI");
  const [paymentDone, setPaymentDone] = useState(false);
  const [paying, setPaying] = useState(false);

  const [form, setForm] = useState({
    age: "",
    gender: "Male",
    height: "",
    weight: "",
    goal: "Muscle Building"
  });

  const updateForm = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };

  const analyzeBody = (e) => {
    e.preventDefault();

    const height = Number(form.height) / 100;
    const weight = Number(form.weight);
    const age = Number(form.age);

    if (!height || !weight || !age || age < 13 || age > 100) {
      alert("Please enter valid details.");
      return;
    }

    const bmi = (weight / (height * height)).toFixed(1);

    const recommendations = {
      "Weight Loss": {
        workout: "Full Body Workout + Cardio",
        schedule: "3 days strength training + 2 days cardio",
        cardio: "Start with 20–30 minutes of brisk walking.",
        membership: "Quarterly Power"
      },
      "Muscle Building": {
        workout: "Beginner Push / Pull / Legs",
        schedule: "3 days strength training + 1–2 recovery days",
        cardio: "Add 10–15 minutes of light cardio.",
        membership: "Annual Elite"
      },
      "Endurance": {
        workout: "Cardio + Functional Training",
        schedule: "3 cardio sessions + 2 strength sessions",
        cardio: "Start with 15–20 minutes of easy cycling.",
        membership: "Quarterly Power"
      },
      "General Fitness": {
        workout: "Balanced Full Body Training",
        schedule: "3 full-body sessions per week",
        cardio: "Walk, cycle or swim 20 minutes.",
        membership: "Monthly Pass"
      }
    };

    setResult({
      bmi,
      ...recommendations[form.goal]
    });
  };

  const openPayment = (plan) => {
    setSelectedPlan(plan);
    setPaymentDone(false);
    setPaying(false);
  };

  const completePayment = () => {
    setPaying(true);

    // DEMO ONLY: No real payment is processed.
    setTimeout(() => {
      setPaying(false);
      setPaymentDone(true);
    }, 1500);
  };

  const closePayment = () => {
    setSelectedPlan(null);
    setPaymentDone(false);
    setPaying(false);
  };

  const navLinks = [
    ["Home", "#home"],
    ["About Us", "#about"],
    ["Workouts", "#workouts"],
    ["Membership", "#membership"],
    ["Body Analyzer & Start", "#analyzer"],
    ["Contact Us", "#contact"]
  ];

  return (
    <div className="min-h-screen overflow-x-hidden">

      {/* NAVBAR */}
      <header className="fixed top-0 w-full z-50 bg-[#090b10]/95 backdrop-blur-xl border-b border-white/10">
        <div className="max-w-7xl mx-auto px-5 py-4 flex items-center justify-between">

          <a href="#home" className="flex items-center gap-2">
            <div className="neon-bg p-2 rounded-lg">
              <Dumbbell size={25}/>
            </div>
            <span className="text-xl font-black italic">
              POWER<span className="neon">PLUS</span>
              <span className="block text-[9px] tracking-[5px] text-gray-400">
                FITNESS CLUB
              </span>
            </span>
          </a>

          <nav className="hidden lg:flex items-center gap-6 text-sm text-gray-300">
            {navLinks.map(([name, link]) => (
              <a key={name} href={link}
                className="hover:text-[#dfff00] transition">
                {name}
              </a>
            ))}
          </nav>

          <a href="#membership"
            className="hidden lg:block neon-bg px-6 py-3 rounded font-bold hover:bg-white transition">
            JOIN NOW <ArrowRight size={16} className="inline"/>
          </a>

          <button className="lg:hidden"
            onClick={() => setMobileMenu(!mobileMenu)}>
            {mobileMenu ? <X/> : <Menu/>}
          </button>
        </div>

        {mobileMenu && (
          <div className="lg:hidden bg-[#11141c] p-5 space-y-5">
            {navLinks.map(([name, link]) => (
              <a key={name} href={link}
                onClick={() => setMobileMenu(false)}
                className="block text-gray-300 hover:text-[#dfff00]">
                {name}
              </a>
            ))}
            <a href="#membership" className="block neon-bg p-3 text-center font-bold">
              JOIN NOW
            </a>
          </div>
        )}
      </header>

      {/* HERO */}
      <section id="home" className="hero-bg min-h-[750px] flex items-center pt-24">
        <div className="max-w-7xl mx-auto px-6 w-full">
          <div className="max-w-3xl">

            <div className="inline-flex items-center gap-2 glass px-4 py-2 rounded-full mb-7">
              <Zap size={16} className="neon"/>
              <span className="text-sm tracking-widest uppercase">
                Your Fitness. Your Power.
              </span>
            </div>

            <h1 className="text-5xl sm:text-6xl md:text-8xl font-black uppercase leading-[1.05]">
              UNLEASH YOUR
              <span className="neon block">ULTIMATE</span>
              POWER.
            </h1>

            <p className="text-gray-300 text-lg mt-7 max-w-xl leading-relaxed">
              Transform your body with state-of-the-art equipment,
              expert trainers, and personalized fitness plans.
            </p>

            <div className="flex flex-wrap gap-4 mt-9">
              <a href="#analyzer"
                className="neon-bg px-8 py-4 rounded font-black hover:bg-white transition">
                START YOUR JOURNEY <ArrowRight className="inline ml-2"/>
              </a>

              <a href="#membership"
                className="border border-white/40 px-8 py-4 rounded font-bold hover:border-[#dfff00] hover:text-[#dfff00] transition">
                EXPLORE PLANS
              </a>
            </div>

            <div className="grid grid-cols-3 gap-5 max-w-lg mt-16">
              <div>
                <h3 className="text-3xl font-black neon">500+</h3>
                <p className="text-xs text-gray-400">Active Members</p>
              </div>
              <div>
                <h3 className="text-3xl font-black neon">15+</h3>
                <p className="text-xs text-gray-400">Expert Trainers</p>
              </div>
              <div>
                <h3 className="text-3xl font-black neon">24/7</h3>
                <p className="text-xs text-gray-400">Fitness Support</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* FEATURES */}
      <section className="py-20 px-6">
        <div className="max-w-7xl mx-auto grid md:grid-cols-3 gap-6">
          {[
            [Dumbbell, "Premium Equipment", "Train with modern equipment designed for every fitness level."],
            [Users, "Expert Trainers", "Get professional guidance and personalized training."],
            [Activity, "Smart Fitness", "Track your progress and achieve measurable results."]
          ].map(([Icon, title, desc]) => (
            <div key={title} className="glass p-8 rounded-xl card-hover">
              <Icon size={35} className="neon mb-5"/>
              <h3 className="text-xl font-bold mb-3">{title}</h3>
              <p className="text-gray-400 leading-relaxed">{desc}</p>
            </div>
          ))}
        </div>
      </section>

      {/* ABOUT */}
      <section id="about" className="py-24 bg-[#10131b]">
        <div className="max-w-7xl mx-auto px-6 grid md:grid-cols-2 gap-14 items-center">
          <div>
            <img
              src="https://images.unsplash.com/photo-1534438327276-14e5300c3a48?w=900"
              alt="PowerPlus gym interior"
              className="rounded-2xl w-full h-[420px] object-cover"
            />
          </div>

          <div>
            <p className="neon font-bold tracking-widest mb-4">ABOUT POWERPLUS</p>
            <h2 className="text-4xl md:text-5xl font-black uppercase">
              BUILD YOUR BODY.
              <span className="neon"> BUILD YOUR LEGACY.</span>
            </h2>
            <p className="text-gray-400 mt-6 leading-relaxed">
              PowerPlus Gym is built around one simple mission:
              helping people become stronger, healthier and more confident.
              We combine modern equipment, experienced coaches and
              personalized fitness programs to make every workout count.
            </p>

            <div className="space-y-4 mt-8">
              {[
                "Certified fitness professionals",
                "Personalized fitness programs",
                "Modern strength and cardio equipment",
                "Friendly and motivating environment"
              ].map(item => (
                <div key={item} className="flex gap-3 items-center">
                  <Check className="neon" size={20}/>
                  <span>{item}</span>
                </div>
              ))}
            </div>

            <a href="#trainers"
              className="inline-block neon-bg px-7 py-4 rounded mt-9 font-bold">
              MEET OUR TRAINERS
            </a>
          </div>
        </div>
      </section>

      {/* WORKOUTS */}
      <section id="workouts" className="py-24 px-6">
        <div className="max-w-7xl mx-auto">
          <div className="text-center mb-14">
            <p className="neon tracking-widest font-bold">TRAIN SMARTER</p>
            <h2 className="text-4xl md:text-5xl font-black mt-3">
              CHOOSE YOUR <span className="neon">WORKOUT</span>
            </h2>
          </div>

          <div className="grid sm:grid-cols-2 lg:grid-cols-4 gap-6">
            {[
              ["Strength Training", "https://images.unsplash.com/photo-1583454110551-21f2fa2afe61?w=600"],
              ["Weight Loss", "https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?w=600"],
              ["Cardio Fitness", "https://images.unsplash.com/photo-1538805060514-97d9cc17730c?w=600"],
              ["Muscle Building", "https://images.unsplash.com/photo-1581009146145-b5ef050c2e1e?w=600"]
            ].map(([name, image]) => (
              <a href="#analyzer" key={name}
                className="relative group overflow-hidden rounded-xl h-80">
                <img src={image} alt={name}
                  className="w-full h-full object-cover group-hover:scale-110 transition duration-500"/>
                <div className="absolute inset-0 bg-gradient-to-t from-black via-black/10 to-transparent"/>
                <h3 className="absolute bottom-7 left-6 text-2xl font-black">
                  {name}
                  <ChevronRight className="inline neon"/>
                </h3>
              </a>
            ))}
          </div>
        </div>
      </section>

      {/* BODY ANALYZER */}
      <section id="analyzer" className="py-24 px-6 bg-[#10131b]">
        <div className="max-w-6xl mx-auto">

          <div className="text-center mb-12">
            <p className="neon font-bold tracking-widest">SMART FITNESS TECHNOLOGY</p>
            <h2 className="text-4xl md:text-5xl font-black mt-3">
              BODY <span className="neon">ANALYZER</span>
            </h2>
            <p className="text-gray-400 mt-4">
              Enter your details to get a beginner fitness recommendation.
            </p>
          </div>

          <div className="grid md:grid-cols-2 gap-8">
            <form onSubmit={analyzeBody}
              className="glass p-7 md:p-10 rounded-2xl space-y-5">

              {[
                ["Age", "age", "number", "Enter your age"],
                ["Height (cm)", "height", "number", "e.g. 175"],
                ["Weight (kg)", "weight", "number", "e.g. 70"]
              ].map(([label, name, type, placeholder]) => (
                <div key={name}>
                  <label className="block text-sm text-gray-300 mb-2">{label}</label>
                  <input
                    type={type}
                    name={name}
                    min="1"
                    max={name === "age" ? "100" : undefined}
                    required
                    value={form[name]}
                    onChange={updateForm}
                    placeholder={placeholder}
                    className="w-full bg-[#090b10] border border-white/10 rounded-lg p-4"
                  />
                </div>
              ))}

              <div>
                <label className="block mb-2 text-sm">Gender</label>
                <select name="gender" value={form.gender}
                  onChange={updateForm}
                  className="w-full bg-[#090b10] border border-white/10 rounded-lg p-4">
                  <option>Male</option>
                  <option>Female</option>
                  <option>Other</option>
                  <option>Prefer not to say</option>
                </select>
              </div>

              <div>
                <label className="block mb-2 text-sm">Fitness Goal</label>
                <select name="goal" value={form.goal}
                  onChange={updateForm}
                  className="w-full bg-[#090b10] border border-white/10 rounded-lg p-4">
                  <option>Muscle Building</option>
                  <option>Weight Loss</option>
                  <option>Endurance</option>
                  <option>General Fitness</option>
                </select>
              </div>

              <button className="neon-bg w-full p-4 rounded-lg font-black hover:bg-white transition">
                ANALYZE MY BODY <Activity className="inline ml-2"/>
              </button>
            </form>

            <div className="glass rounded-2xl p-8 flex flex-col justify-center">
              {!result ? (
                <div className="text-center">
                  <div className="mx-auto w-20 h-20 rounded-full bg-[#dfff00]/10 flex items-center justify-center mb-6">
                    <Activity size={40} className="neon"/>
                  </div>
                  <h3 className="text-2xl font-black">YOUR RESULTS HERE</h3>
                  <p className="text-gray-400 mt-3">
                    Complete the form to unlock your personalized
                    beginner workout plan.
                  </p>
                </div>
              ) : (
                <div>
                  <p className="neon font-bold tracking-widest">YOUR FITNESS REPORT</p>
                  <h3 className="text-3xl font-black mt-3">LET'S GET STRONGER!</h3>

                  <div className="bg-[#090b10] rounded-xl p-5 mt-6">
                    <p className="text-gray-400 text-sm">Estimated BMI</p>
                    <p className="text-4xl neon font-black">{result.bmi}</p>
                    <p className="text-xs text-gray-500 mt-2">
                      BMI is a screening measure, not a diagnosis or complete body analysis.
                    </p>
                  </div>

                  <div className="mt-6 space-y-4">
                    <div>
                      <p className="text-gray-400 text-sm">Recommended Workout</p>
                      <p className="font-bold">{result.workout}</p>
                    </div>
                    <div>
                      <p className="text-gray-400 text-sm">Weekly Schedule</p>
                      <p className="font-bold">{result.schedule}</p>
                    </div>
                    <div>
                      <p className="text-gray-400 text-sm">Cardio Recommendation</p>
                      <p className="font-bold">{result.cardio}</p>
                    </div>
                    <div>
                      <p className="text-gray-400 text-sm">Suggested Membership</p>
                      <p className="neon font-black">{result.membership}</p>
                    </div>
                  </div>

                  <a href="#membership"
                    className="block text-center neon-bg p-4 rounded mt-7 font-bold">
                    EXPLORE MEMBERSHIP <ArrowRight className="inline"/>
                  </a>
                </div>
              )}
            </div>
          </div>
          <p className="text-xs text-gray-500 mt-5 text-center">
            Beginner suggestions only. Consult a qualified trainer or healthcare professional
            before starting an exercise program, especially if you have health concerns.
          </p>
        </div>
      </section>

      {/* MEMBERSHIP */}
      <section id="membership" className="py-24 px-6">
        <div className="max-w-7xl mx-auto">
          <div className="text-center mb-16">
            <p className="neon tracking-widest font-bold">INVEST IN YOURSELF</p>
            <h2 className="text-4xl md:text-5xl font-black mt-3">
              MEMBERSHIP <span className="neon">PLANS</span>
            </h2>
            <p className="text-gray-400 mt-4">
              Choose a plan that matches your fitness goals.
            </p>
          </div>

          <div className="grid md:grid-cols-3 gap-8">
            {plans.map(plan => (
              <div key={plan.name}
                className={`relative glass rounded-2xl p-8 card-hover ${
                  plan.popular ? "border-[#dfff00]" : ""
                }`}>
                {plan.popular && (
                  <div className="absolute -top-4 left-1/2 -translate-x-1/2 neon-bg px-5 py-2 text-xs font-black rounded-full">
                    MOST POPULAR
                  </div>
                )}

                <h3 className="text-2xl font-black mt-3">{plan.name}</h3>
                <p className="text-gray-400 text-sm mt-2">{plan.description}</p>

                <div className="mt-8 mb-8">
                  <span className="text-4xl font-black neon">₹{plan.price.toLocaleString("en-IN")}</span>
                  <span className="text-gray-400"> / {plan.duration}</span>
                </div>

                <div className="border-t border-white/10 pt-7 space-y-5">
                  {plan.benefits.map(benefit => (
                    <div key={benefit} className="flex items-center gap-3">
