# ------------------------
# 1️⃣ إنشاء مجلد المشروع والمجلدات الفرعية
mkdir -p ai-content-review-mvp/pages/api/auth ai-content-review-mvp/pages/auth ai-content-review-mvp/pages/components ai-content-review-mvp/styles ai-content-review-mvp/public/images
cd ai-content-review-mvp

# ------------------------
# 2️⃣ package.json
cat > package.json <<EOL
{
  "name": "ai-content-review-mvp",
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "dependencies": {
    "next": "13.5.4",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "tailwindcss": "^3.3.3",
    "pdf-lib": "^1.17.1",
    "react-dropzone": "^14.2.3",
    "openai": "^4.33.0",
    "next-auth": "^4.26.1",
    "@stripe/stripe-js": "^2.1.0",
    "stripe": "^12.11.0",
    "bcrypt": "^5.1.0",
    "@heroicons/react": "^2.0.18"
  }
}
EOL

# ------------------------
# 3️⃣ tailwind.config.js
cat > tailwind.config.js <<EOL
module.exports = {
  content: ['./pages/**/*.{js,ts,jsx,tsx}', './components/**/*.{js,ts,jsx,tsx}'],
  theme: { extend: {} },
  plugins: [],
}
EOL

# ------------------------
# 4️⃣ .env.local
cat > .env.local <<EOL
OPENAI_API_KEY=ضع_مفتاحك_هنا
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=ضع_سر_التشفير_هنا
STRIPE_SECRET_KEY=ضع_مفتاح_Stripe_هنا
EOL

# ------------------------
# 5️⃣ styles/globals.css
cat > styles/globals.css <<EOL
@tailwind base;
@tailwind components;
@tailwind utilities;
EOL

# ------------------------
# 6️⃣ Landing Page النهائي: pages/index.tsx
cat > pages/index.tsx <<EOL
import Link from "next/link";
import { CheckIcon, LightningBoltIcon, ChartBarIcon } from "@heroicons/react/24/solid";

export default function Home() {
  return (
    <div className="min-h-screen flex flex-col bg-gradient-to-br from-indigo-50 via-white to-purple-50">
      <header className="flex justify-between items-center p-6 max-w-6xl mx-auto">
        <h1 className="text-3xl font-bold text-indigo-700">AI Content Review</h1>
        <div className="flex gap-4">
          <Link href="/auth/signin" className="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700 transition">تسجيل الدخول</Link>
          <Link href="/dashboard" className="bg-green-600 text-white px-4 py-2 rounded hover:bg-green-700 transition">لوحة التحكم</Link>
        </div>
      </header>

      <section className="flex flex-col items-center text-center px-4 py-20 space-y-6 max-w-4xl mx-auto">
        <h2 className="text-5xl font-extrabold text-gray-800">حسّن محتواك قبل النشر باستخدام الذكاء الاصطناعي</h2>
        <p className="text-gray-600 text-lg">اكتشف نقاط القوة والضعف في مقالاتك، فيديوهاتك، وعناوينك قبل أن يراها الجمهور. احصل على تقرير شامل مع اقتراحات دقيقة لتحسين الأداء والجاذبية.</p>
        <Link href="/auth/signin" className="bg-gradient-to-r from-purple-600 to-indigo-600 text-white px-8 py-4 rounded-lg text-lg font-semibold hover:from-purple-700 hover:to-indigo-700 transition">ابدأ الآن مجانًا</Link>
      </section>

      <section className="bg-white py-16">
        <div className="max-w-6xl mx-auto px-4 grid md:grid-cols-3 gap-8">
          <div className="p-6 border rounded-xl shadow hover:shadow-lg transition flex flex-col items-center text-center gap-4">
            <LightningBoltIcon className="w-12 h-12 text-indigo-600" />
            <h3 className="text-xl font-bold">تحليل العنوان والجاذبية</h3>
            <img src="/images/feature1.svg" alt="Feature 1" className="w-32 h-32"/>
            <p>نقد شامل لعناوينك وصورك المصغرة لمعرفة مدى جذبها للجمهور المستهدف.</p>
          </div>
          <div className="p-6 border rounded-xl shadow hover:shadow-lg transition flex flex-col items-center text-center gap-4">
            <ChartBarIcon className="w-12 h-12 text-indigo-600" />
            <h3 className="text-xl font-bold">تقييم المحتوى والنبرة</h3>
            <img src="/images/feature2.svg" alt="Feature 2" className="w-32 h-32"/>
            <p>تحليل شامل لنبرة المحتوى، الأسلوب، هيكل الأفكار، وسلاسة العرض.</p>
          </div>
          <div className="p-6 border rounded-xl shadow hover:shadow-lg transition flex flex-col items-center text-center gap-4">
            <CheckIcon className="w-12 h-12 text-indigo-600" />
            <h3 className="text-xl font-bold">اقتراحات تحسين دقيقة</h3>
            <img src="/images/feature3.svg" alt="Feature 3" className="w-32 h-32"/>
            <p>نصائح عملية قابلة للتنفيذ لتقوية نقاط المحتوى الضعيفة وزيادة فرص النجاح.</p>
          </div>
        </div>
      </section>

      <section className="py-16 bg-gradient-to-r from-purple-100 to-indigo-100 text-center">
        <h3 className="text-3xl font-bold mb-4">ارتقِ بمحتواك إلى المستوى الاحترافي</h3>
        <p className="text-gray-700 mb-6">اشترك في النسخة الاحترافية واستفد من تقارير موسعة، دعم فني، وتحليلات متقدمة.</p>
        <form method="POST" action="/api/checkout" className="inline-block">
          <input type="hidden" name="priceId" value="price_xxxxxxxx" />
          <button type="submit" className="bg-indigo-600 text-white px-8 py-4 rounded-lg text-lg font-semibold hover:bg-indigo-700 transition">اشترك الآن Pro</button>
        </form>
      </section>

      <footer className="bg-gray-800 text-white py-6 mt-auto text-center">
        <p>&copy; 2025 AI Content Review. جميع الحقوق محفوظة.</p>
      </footer>
    </div>
  );
}
EOL

# ------------------------
# 7️⃣ إنشاء صور SVG وهمية لكل ميزة
cat > public/images/feature1.svg <<EOL
<svg xmlns="http://www.w3.org/2000/svg" width="128" height="128" fill="none" stroke="purple"><circle cx="64" cy="64" r="60" stroke-width="4"/></svg>
EOL

cat > public/images/feature2.svg <<EOL
<svg xmlns="http://www.w3.org/2000/svg" width="128" height="128" fill="none" stroke="purple"><rect x="16" y="16" width="96" height="96" stroke-width="4"/></svg>
EOL

cat > public/images/feature3.svg <<EOL
<svg xmlns="http://www.w3.org/2000/svg" width="128" height="128" fill="none" stroke="purple"><polygon points="64,8 120,120 8,120" stroke-width="4"/></svg>
EOL

# ------------------------
# 8️⃣ بقية الملفات مثل dashboard.tsx و api/analyze.ts و checkout.ts و auth كما في السكربت السابق
# يمكنك إضافةهم بنفس الطريقة أو استخدام السكربت السابق.

# ------------------------
# العودة للمجلد الأب وإنشاء ZIP كامل
cd ..
zip -r ai-content-review-mvp-final.zip ai-content-review-mvp

echo "✅ تم إنشاء المشروع النهائي مع Landing Page المحسّنة بصريًا وملف ZIP جاهز: ai-content-review-mvp-final.zip"
