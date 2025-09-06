---
transition: view-transition
---

# How TypeScript compiles

<div class="compilation-phases-container">
  <div v-click="1" class="phase-box parse-phase">
    <h3>Parse</h3>
    <div class="phase-description">
      Source code → AST<br>
      Import resolution<br>
      Syntax errors
    </div>
    <!-- Individual files that appear and expand within the Parse phase -->
    <div class="file-grid">
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 100 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 200 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 300 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 400 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 500 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 600 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 700 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 800 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 900 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1000 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1100 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1200 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1300 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1400 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1500 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1600 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1700 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1800 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 1900 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2000 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2100 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2200 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2300 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2400 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2500 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2600 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2700 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2800 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 2900 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 3000 } }" class="file-box"></div>
      <div v-motion v-click="5" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-5="{ transition: { delay: 3100 } }" class="file-box"></div>
    </div>
  </div>
  <div v-click="2" class="arrow">→</div>
  <div v-click="2" class="phase-box bind-phase">
    <h3>Bind</h3>
    <div class="phase-description">
      Symbol creation<br>
      Scope analysis<br>
      Control flow graphs
    </div>
    <!-- Files expand in Bind phase -->
    <div class="file-grid">
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 100 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 200 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 300 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 400 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 500 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 600 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 700 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 800 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 900 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1000 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1100 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1200 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1300 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1400 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1500 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1600 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1700 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1800 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 1900 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2000 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2100 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2200 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2300 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2400 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2500 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2600 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2700 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2800 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 2900 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 3000 } }" class="file-box"></div>
      <div v-motion v-click="6" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-6="{ transition: { delay: 3100 } }" class="file-box"></div>
    </div>
  </div>
  <div v-click="3" class="arrow">→</div>
  <div v-click="3" class="phase-box check-phase">
    <h3>Check</h3>
    <div class="phase-description">
      Type checking<br>
      Reference analysis<br>
      Error detection
    </div>
    <!-- Files expand in Check phase -->
    <div class="file-grid">
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 100 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 200 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 300 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 400 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 500 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 600 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 700 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 800 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 900 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1000 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1100 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1200 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1300 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1400 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1500 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1600 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1700 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1800 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 1900 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2000 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2100 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2200 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2300 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2400 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2500 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2600 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2700 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2800 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 2900 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 3000 } }" class="file-box"></div>
      <div v-motion v-click="7" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-7="{ transition: { delay: 3100 } }" class="file-box"></div>
    </div>
  </div>
  <div v-click="4" class="arrow">→</div>
  <div v-click="4" class="phase-box emit-phase">
    <h3>Emit</h3>
    <div class="phase-description">
      TS → JS<br>
      Syntax downleveling<br>
      File writing
    </div>
    <!-- Files expand in Emit phase -->
    <div class="file-grid">
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 100 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 200 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 300 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 400 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 500 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 600 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 700 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 800 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 900 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1000 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1100 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1200 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1300 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1400 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1500 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1600 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1700 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1800 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 1900 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2000 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2100 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2200 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2300 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2400 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2500 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2600 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2700 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2800 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 2900 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 3000 } }" class="file-box"></div>
      <div v-motion v-click="8" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" :click-8="{ transition: { delay: 3100 } }" class="file-box"></div>
    </div>
  </div>
</div>

<style>
.compilation-phases-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 90%;
  margin: 10% auto;
  gap: 3%;
}

.phase-box {
  width: 18%;
  height: 270px;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  position: relative;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
  padding: 15px 5px 40px 5px;
  overflow: visible;
}

.parse-phase {
  background: linear-gradient(135deg, #4f46e5, #6366f1);
  color: white;
}

.bind-phase {
  background: linear-gradient(135deg, #059669, #10b981);
  color: white;
}

.check-phase {
  background: linear-gradient(135deg, #dc2626, #ef4444);
  color: white;
}

.emit-phase {
  background: linear-gradient(135deg, #7c2d12, #ea580c);
  color: white;
}

.phase-box h3 {
  margin: 0 0 8px 0;
  font-size: 1.3rem;
  font-weight: bold;
}

.phase-description {
  text-align: center;
  font-size: 0.8rem;
  line-height: 1.3;
  opacity: 0.9;
  margin-bottom: 10px;
}

.file-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(8, 1fr);
  gap: 3px;
  align-items: center;
  width: 100%;
  height: 120px;
  margin-bottom: 15px;
  padding: 0 8px;
}

.file-box {
  background: rgba(255, 255, 255, 0.3);
  border-radius: 2px;
  height: 12px;
  width: 100%;
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.arrow {
  font-size: 2rem;
  font-weight: bold;
  color: var(--slidev-theme-primary);
  opacity: 0.7;
}

/* Dark mode adjustments */
.dark .phase-box {
  box-shadow: 0 4px 15px rgba(255,255,255,0.1);
}
</style>

<!--
To understand how we make use of concurrency, we first need to look at how TypeScript compiles code.

The first phase is parsing. In this phase, we read all of the files the user specifies,
resolve their imports, parse more files, and so on, until everything is loaded.

Next is binding. In this phase, we walk all of the ASTs, collecting symbol information,
scopes, and build control flow graphs, attaching that info to the ASTs.

Then we check the files, walking each of them, verifying that the program is correct.

Lastly, we emit the files, erasing types, transforming the syntax to support older
runtimes, then write the files out to disk.

Now, in the old compiler, we had to do all of this in a single thread. That meant
we parsed files one after the other

Then bound each file one after the other,

Then checked each file one after the other,

You get the picture.

We can't do any better than this because JavaScript does not have a way to share
objects between threads. If we tried to do this in parallel, sure we could parse in parallel,
but then we'd have to serialize the data across the thread, and that can take more time
than just parsing the file!
-->

---

# How TypeScript compiles _concurrently_

<div class="compilation-phases-container">
  <div class="phase-box parse-phase">
    <h3>Parse</h3>
    <div class="phase-description">
      Source code → AST<br>
      Import resolution<br>
      Syntax errors
    </div>
    <!-- Individual files that appear and expand within the Parse phase with random delays for concurrency -->
    <div class="file-grid">
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 150 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 320 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 80 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 420 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 200 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 680 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 30 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 850 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 560 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 120 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 780 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 380 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 950 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 480 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 620 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 180 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 720 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 520 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 280 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1100 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 50 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 890 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 350 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 750 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 450 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1020 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 590 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 820 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 250 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 980 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 680 } }" class="file-box"></div>
      <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 410 } }" class="file-box"></div>
    </div>
  </div>
  <div class="arrow">→</div>
  <div class="phase-box bind-phase">
    <h3>Bind</h3>
    <div class="phase-description">
      Symbol creation<br>
      Scope analysis<br>
      Control flow graphs
    </div>
    <!-- Files expand in Bind phase with random delays for concurrency -->
    <div class="file-grid">
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 680 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 120 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 890 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 340 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 750 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 50 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 960 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 220 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 580 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 810 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 180 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 720 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 480 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1050 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 400 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 660 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 280 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 930 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 520 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 140 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 850 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 370 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 780 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 320 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1120 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 620 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 90 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 760 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 440 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1000 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 580 } }" class="file-box"></div>
      <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 250 } }" class="file-box"></div>
    </div>
  </div>
  <div class="arrow">→</div>
  <div class="phase-box check-phase">
    <h3>Check</h3>
    <div class="phase-description">
      Type checking<br>
      Reference analysis<br>
      Error detection
    </div>
    <!-- Big question mark appears in Check phase -->
    <div v-motion v-click="4" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1 }" class="question-mark">?</div>
  </div>
  <div class="arrow">→</div>
  <div class="phase-box emit-phase">
    <h3>Emit</h3>
    <div class="phase-description">
      TS → JS<br>
      Syntax downleveling<br>
      File writing
    </div>
    <!-- Files expand in Emit phase -->
    <div class="file-grid">
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 450 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 180 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 920 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 60 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 740 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 290 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1080 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 520 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 210 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 870 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 390 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 650 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 140 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1150 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 480 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 800 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 320 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 960 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 580 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 110 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 770 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 430 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1020 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 250 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 690 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 840 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 360 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1200 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 510 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 90 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 720 } }" class="file-box"></div>
      <div v-motion v-click="3" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 990 } }" class="file-box"></div>
    </div>
  </div>
</div>

<style>
.compilation-phases-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 90%;
  margin: 10% auto;
  gap: 3%;
}

.phase-box {
  width: 18%;
  height: 270px;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  position: relative;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
  padding: 15px 5px 40px 5px;
  overflow: visible;
}

.parse-phase {
  background: linear-gradient(135deg, #4f46e5, #6366f1);
  color: white;
}

.bind-phase {
  background: linear-gradient(135deg, #059669, #10b981);
  color: white;
}

.check-phase {
  background: linear-gradient(135deg, #dc2626, #ef4444);
  color: white;
}

.emit-phase {
  background: linear-gradient(135deg, #7c2d12, #ea580c);
  color: white;
}

.phase-box h3 {
  margin: 0 0 8px 0;
  font-size: 1.3rem;
  font-weight: bold;
}

.phase-description {
  text-align: center;
  font-size: 0.8rem;
  line-height: 1.3;
  opacity: 0.9;
  margin-bottom: 10px;
}

.file-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(8, 1fr);
  gap: 3px;
  align-items: center;
  width: 100%;
  height: 120px;
  margin-bottom: 15px;
  padding: 0 8px;
}

.file-box {
  background: rgba(255, 255, 255, 0.3);
  border-radius: 2px;
  height: 12px;
  width: 100%;
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.arrow {
  font-size: 2rem;
  font-weight: bold;
  color: var(--slidev-theme-primary);
  opacity: 0.7;
}

.question-mark {
  font-size: 4rem;
  font-weight: bold;
  color: rgba(255, 255, 255, 0.9);
  text-align: center;
  flex-grow: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
}

/* Dark mode adjustments */
.dark .phase-box {
  box-shadow: 0 4px 15px rgba(255,255,255,0.1);
}
</style>

<!--
But in the new Go powered compiler, we can do better.

Parsing a file does not depend on anything else, so we can parse many files we want at once.

Binding a file is also self-contained, so we can do that in parallel too.

File emitting is also self-contained, so once again, we are now able to do that in parallel.


Type checking/evaluation is a complicated process.
Information can be pulled from anywhere at any time.
The types from one file can affect what happens in any other file.
Things are order dependent, recursive, etc.

How do you handle concurrency for something like that?
-->

---
layout: none
---

<div class="type-network">
  <div class="main-file-container">
    <div class="ts-file main-file">
      <div class="file-header">📄 app.ts</div>
      <div class="file-content">
        <div class="code-line">import { User } from './user';</div>
        <div class="code-line">import { Database } from './db';</div>
        <div class="code-line">import { Logger, ApiError } from './utils';</div>
        <div class="code-line">import { Status } from './types';</div>
        <div class="code-line"></div>
        <div class="code-line">class AppService {</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;private db: Database;</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;private logger: Logger;</div>
        <div class="code-line"></div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;constructor(<span :class="$clicks >= 1 && $clicks < 6 ? 'highlight' : ''">db: Database</span>, <span :class="$clicks >= 3 && $clicks < 6 ? 'highlight-green' : ''">logger: Logger</span>) {</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span :class="$clicks >= 3 && $clicks < 6 ? 'highlight' : ''">this.db = db;</span></div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span :class="$clicks >= 5 && $clicks < 6 ? 'highlight-green' : ''">this.logger = logger;</span></div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
        <div class="code-line"></div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;async getUser(id: string): Promise&lt;User&gt; {</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.logger.info('Fetching user: ' + id);</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;const user = await this.db.findUser(id);</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (!user) {</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;throw new <span :class="$clicks >= 8 ? 'highlight-purple' : ''">ApiError</span>('User not found');</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return user;</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
        <div class="code-line"></div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;async updateStatus(id: string, status: Status) {</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;const user = await this.getUser(id);</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;user.status = status;</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;await this.db.saveUser(user);</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
        <div class="code-line">}</div>
      </div>
    </div>
  </div>
  <div class="dependency-grid">
    <div class="ts-file dep-file">
      <div class="file-header">📄 user.ts</div>
      <div class="file-content">
        <div class="code-line">import { Status } from './types';</div>
        <div class="code-line">export interface User {</div>
        <div class="code-line">&nbsp;&nbsp;id: string;</div>
        <div class="code-line">&nbsp;&nbsp;name: string;</div>
        <div class="code-line">&nbsp;&nbsp;email: string;</div>
        <div class="code-line">&nbsp;&nbsp;status: Status;</div>
        <div class="code-line">&nbsp;&nbsp;preferences: UserPrefs;</div>
        <div class="code-line">}</div>
        <div class="code-line">export interface UserPrefs {</div>
        <div class="code-line">&nbsp;&nbsp;theme: 'light' | 'dark';</div>
        <div class="code-line">&nbsp;&nbsp;lang: string;</div>
        <div class="code-line">}</div>
      </div>
    </div>
    <div class="ts-file dep-file">
      <div class="file-header">📄 db.ts</div>
      <div class="file-content">
        <div class="code-line">import { User } from './user';</div>
        <div class="code-line">import { Logger } from './utils';</div>
        <div class="code-line">import { Config } from './types';</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">export class Database {</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">&nbsp;&nbsp;constructor(</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">&nbsp;&nbsp;&nbsp;&nbsp;private config: Config,</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">&nbsp;&nbsp;&nbsp;&nbsp;private logger: Logger</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">&nbsp;&nbsp;) {}</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">&nbsp;&nbsp;async findUser(id: string):</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">&nbsp;&nbsp;&nbsp;&nbsp;Promise&lt;User | null&gt; {}</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">&nbsp;&nbsp;async saveUser(u: User) {}</div>
        <div class="code-line" :class="$clicks >= 2 && $clicks < 6 ? 'highlight' : ''">}</div>
      </div>
    </div>
    <div class="ts-file dep-file">
      <div class="file-header">📄 utils.ts</div>
      <div class="file-content">
        <div class="code-line">import { UserPrefs } from './user';</div>
        <div class="code-line">import { Event } from './events';</div>
        <div class="code-line" :class="$clicks >= 4 && $clicks < 6 ? 'highlight-green' : ''">export interface Logger {</div>
        <div class="code-line" :class="$clicks >= 4 && $clicks < 6 ? 'highlight-green' : ''">&nbsp;&nbsp;info(msg: string): void;</div>
        <div class="code-line" :class="$clicks >= 4 && $clicks < 6 ? 'highlight-green' : ''">&nbsp;&nbsp;error(msg: string): void;</div>
        <div class="code-line" :class="$clicks >= 4 && $clicks < 6 ? 'highlight-green' : ''">&nbsp;&nbsp;debug(msg: string,</div>
        <div class="code-line" :class="$clicks >= 4 && $clicks < 6 ? 'highlight-green' : ''">&nbsp;&nbsp;&nbsp;&nbsp;prefs?: UserPrefs): void;</div>
        <div class="code-line" :class="$clicks >= 4 && $clicks < 6 ? 'highlight-green' : ''">}</div>
        <div class="code-line" :class="$clicks >= 9 ? 'highlight-purple' : ''">export class ApiError extends Error {</div>
        <div class="code-line" :class="$clicks >= 9 ? 'highlight-purple' : ''">&nbsp;&nbsp;constructor(message: string) {</div>
        <div class="code-line" :class="$clicks >= 9 ? 'highlight-purple' : ''">&nbsp;&nbsp;&nbsp;&nbsp;super(message);</div>
        <div class="code-line" :class="$clicks >= 9 ? 'highlight-purple' : ''">&nbsp;&nbsp;&nbsp;&nbsp;this.name = 'ApiError';</div>
        <div class="code-line" :class="$clicks >= 9 ? 'highlight-purple' : ''">&nbsp;&nbsp;}</div>
        <div class="code-line" :class="$clicks >= 9 ? 'highlight-purple' : ''">}</div>
      </div>
    </div>
    <div class="ts-file dep-file">
      <div class="file-header">📄 types.ts</div>
      <div class="file-content">
        <div class="code-line">export type Status =</div>
        <div class="code-line">&nbsp;&nbsp;'active' | 'inactive' |</div>
        <div class="code-line">&nbsp;&nbsp;'pending' | 'suspended';</div>
        <div class="code-line">export interface Config {</div>
        <div class="code-line">&nbsp;&nbsp;apiUrl: string;</div>
        <div class="code-line">&nbsp;&nbsp;timeout: number;</div>
        <div class="code-line">&nbsp;&nbsp;retries: number;</div>
        <div class="code-line">}</div>
        <div class="code-line">export type EventType =</div>
        <div class="code-line">&nbsp;&nbsp;'user_login' | 'user_logout' |</div>
        <div class="code-line">&nbsp;&nbsp;'data_update' | 'error';</div>
        <div class="code-line">export type Result&lt;T&gt; = T | Error;</div>
      </div>
    </div>
    <div class="ts-file dep-file">
      <div class="file-header">📄 auth.ts</div>
      <div class="file-content">
        <div class="code-line">import { User } from './user';</div>
        <div class="code-line">import { ApiClient } from './api';</div>
        <div class="code-line">import { Result } from './types';</div>
        <div class="code-line">export class AuthService {</div>
        <div class="code-line">&nbsp;&nbsp;constructor(</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;private api: ApiClient</div>
        <div class="code-line">&nbsp;&nbsp;) {}</div>
        <div class="code-line">&nbsp;&nbsp;async login(email: string,</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;pwd: string):</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;Promise&lt;Result&lt;User&gt;&gt; {}</div>
        <div class="code-line">&nbsp;&nbsp;logout(): void {}</div>
        <div class="code-line">}</div>
      </div>
    </div>
    <div class="ts-file dep-file">
      <div class="file-header">📄 events.ts</div>
      <div class="file-content">
        <div class="code-line">import { EventType, Result } from './types';</div>
        <div class="code-line">import { User } from './user';</div>
        <div class="code-line">export interface Event {</div>
        <div class="code-line">&nbsp;&nbsp;id: string;</div>
        <div class="code-line">&nbsp;&nbsp;type: EventType;</div>
        <div class="code-line">&nbsp;&nbsp;timestamp: Date;</div>
        <div class="code-line">&nbsp;&nbsp;payload: unknown;</div>
        <div class="code-line">&nbsp;&nbsp;user?: User;</div>
        <div class="code-line">}</div>
        <div class="code-line">export class EventEmitter {</div>
        <div class="code-line">&nbsp;&nbsp;emit(event: Event): Result&lt;void&gt;</div>
        <div class="code-line">}</div>
      </div>
    </div>
    <div class="ts-file dep-file">
      <div class="file-header">📄 api.ts</div>
      <div class="file-content">
        <div class="code-line">import { Config, Result } from './types';</div>
        <div class="code-line">import { Logger } from './utils';</div>
        <div class="code-line">export class ApiClient {</div>
        <div class="code-line">&nbsp;&nbsp;constructor(</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;private config: Config,</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;private logger: Logger</div>
        <div class="code-line">&nbsp;&nbsp;) {}</div>
        <div class="code-line">&nbsp;&nbsp;async get&lt;T&gt;(url: string):</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;Promise&lt;Result&lt;T&gt;&gt; {}</div>
        <div class="code-line">&nbsp;&nbsp;async post&lt;T&gt;(url: string,</div>
        <div class="code-line">&nbsp;&nbsp;&nbsp;&nbsp;data: unknown): Promise&lt;T&gt;</div>
        <div class="code-line">}</div>
      </div>
    </div>
    <div class="ts-file dep-file">
      <div class="file-header">📄 store.ts</div>
      <div class="file-content">
        <div class="code-line">import { User, UserPrefs } from './user';</div>
        <div class="code-line">import { Event } from './events';</div>
        <div class="code-line">import { Status } from './types';</div>
        <div class="code-line">import { Logger } from './utils';</div>
        <div class="code-line">interface AppState {</div>
        <div class="code-line">&nbsp;&nbsp;user: User | null;</div>
        <div class="code-line">&nbsp;&nbsp;status: Status;</div>
        <div class="code-line">&nbsp;&nbsp;events: Event[];</div>
        <div class="code-line">}</div>
        <div class="code-line">export class Store {</div>
        <div class="code-line">&nbsp;&nbsp;state: AppState;</div>
        <div class="code-line">&nbsp;&nbsp;dispatch(e: Event): void {}</div>
        <div class="code-line">}</div>
      </div>
    </div>
  </div>
  <!-- Type Checker Animation -->
  <div
    v-motion
    :initial="{ opacity: 0, scale: 0 }"
    :click-1="{
      opacity: 1,
      scale: 0.8,
      x: -300,
      y: -40,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    :click-2="{
      x: 180,
      y: -150,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    :click-3="{
      x: -300,
      y: -40,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    :click-4="{
      x: 40,
      y: -50,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    :click-5="{
      x: -300,
      y: -20,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    :click-6="{
      opacity: 0,
      transition: { type: 'keyframes', duration: 300, ease: 'easeInOut' }
    }"
    :click-8="{
      opacity: 1,
	  x: -300,
	  y: -100,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    :click-9="{
      x: 0,
      y: -190,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    :click-10="{
      x: -300,
	  y: -100,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
	:click-11="{
      opacity: 0,
	  x: -600,
	  y: -100,
      transition: { type: 'keyframes', duration: 300, ease: 'easeInOut' }
    }"
	:click-12="{
      opacity: 1,
      x: -300,
	  y: -100,
      transition: { type: 'keyframes', duration: 500, ease: 'easeInOut' }
    }"
    class="type-checker"
  >
    <div class="checker-content">
      <div class="checker-header">Checker</div>
      <div class="type-tables">
        <div class="type-table">
          <div class="table-grid">
            <div class="data-cell data-cell-yellow" v-click="[1,11]"></div>
            <div class="data-cell data-cell-yellow" v-click="[1,11]"></div>
            <div class="data-cell data-cell-yellow" v-click="[2,11]"></div>
            <div class="data-cell data-cell-green" v-click="[3,11]"></div>
            <div class="data-cell data-cell-yellow" v-click="[2,11]"></div>
            <div class="data-cell data-cell-green" v-click="[4,11]"></div>
            <div class="data-cell data-cell-green" v-click="[3,11]"></div>
            <div class="data-cell data-cell-mixed" v-click="[5,11]"></div>
            <div class="data-cell data-cell-purple" v-click="[9,11]"></div>
            <div class="data-cell data-cell-purple" v-click="[9,11]"></div>
          </div>
        </div>
        <div class="type-table">
          <div class="table-grid">
            <div class="data-cell data-cell-yellow" v-click="[2,11]"></div>
            <div class="data-cell data-cell-green" v-click="[3,11]"></div>
            <div class="data-cell data-cell-yellow" v-click="[2,11]"></div>
            <div class="data-cell data-cell-green" v-click="[4,11]"></div>
            <div class="data-cell data-cell-green" v-click="[4,11]"></div>
            <div class="data-cell data-cell-mixed" v-click="[5,11]"></div>
            <div class="data-cell data-cell-purple" v-click="[9,11]"></div>
          </div>
        </div>
        <div class="type-table">
          <div class="table-grid">
            <div class="data-cell data-cell-yellow" v-click="[1,11]"></div>
            <div class="data-cell data-cell-green" v-click="[3,11]"></div>
            <div class="data-cell data-cell-green" v-click="[4,11]"></div>
            <div class="data-cell data-cell-green" v-click="[3,11]"></div>
            <div class="data-cell data-cell-mixed" v-click="[5,11]"></div>
            <div class="data-cell data-cell-mixed" v-click="[5,11]"></div>
            <div class="data-cell data-cell-green" v-click="[4,11]"></div>
            <div class="data-cell data-cell-purple" v-click="[9,11]"></div>
            <div class="data-cell data-cell-purple" v-click="[9,11]"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Hover Box Animation -->
  <div
    v-motion
    :initial="{ opacity: 0, scale: 0 }"
    :click-7="{
      opacity: 1,
      scale: 1,
      x: -150,
      y: 50,
      transition: { type: 'keyframes', duration: 300, ease: 'easeInOut' }
    }"
    class="hover-box"
  >
    <div class="hover-content">
      <div v-if="$clicks < 10" class="loading-text">(loading...)</div>
      <div v-else class="hover-info">
        <div class="hover-title">(class) ApiError</div>
        <div class="hover-separator"></div>
        <div class="hover-description">An Error in the API.</div>
      </div>
    </div>
  </div>
</div>
<!-- Hack: make clicks extend to the right count. -->
<span v-click="12"></span>

<style>
.type-network {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: start;
  justify-content: center;
  padding: 20px;
  margin: 20px auto;
  position: relative;
  max-width: 800px;
}
.main-file-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.dependency-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: repeat(4, 1fr);
  gap: 12px;
  align-items: start;
  justify-items: center;
}
.ts-file {
  background: white;
  border-radius: 6px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.1);
  border: 1px solid #e2e8f0;
  overflow: hidden;
  position: relative;
  max-width: 300px;
}
.main-file {
  border-color: #3b82f6;
  max-width: 400px;
}
.dep-file {
  max-width: 140px;
}
.file-header {
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  color: white;
  padding: 8px 12px;
  font-weight: 600;
  font-size: 12px;
  font-family: var(--slidev-code-font-family);
}
.file-content {
  padding: 10px;
  background: #fafafa;
  font-family: var(--slidev-code-font-family);
  font-size: 11px;
  line-height: 1.3;
}
.dep-file .file-content {
  font-size: 6px;
  line-height: 1.0;
  padding: 6px;
}
.dep-file .file-header {
  padding: 2px 8px;
  font-size: 5px;
  line-height: 1.0;
}
.code-line {
  color: #374151;
  margin: 0;
  white-space: nowrap;
  overflow: hidden;
}
.dark .ts-file {
  background: #0f172a;
  border-color: #475569;
}
.dark .file-content {
  background: #1e293b;
}
.dark .code-line {
  color: #e2e8f0;
}
.highlight {
  background-color: #fbbf24;
  color: #1f2937;
  border-radius: 3px;
  font-weight: 600;
  box-sizing: border-box;
}
.dark .highlight {
  background-color: #f59e0b;
  color: #111827;
}
.highlight-green {
  background-color: #6ee7b7;
  color: #1f2937;
  border-radius: 3px;
  font-weight: 600;
  box-sizing: border-box;
}
.dark .highlight-green {
  background-color: #34d399;
  color: #1f2937;
}
.highlight-purple {
  background-color: #c084fc;
  color: #1f2937;
  border-radius: 3px;
  font-weight: 600;
  box-sizing: border-box;
}
.dark .highlight-purple {
  background-color: #a855f7;
  color: #1f2937;
}
.type-checker {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 10;
  pointer-events: none;
}
.checker-content {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 10px 16px 16px 16px;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.4);
  font-family: var(--slidev-code-font-family);
  min-width: 280px;
  border: 2px solid rgba(255, 255, 255, 0.2);
}
.checker-header {
  font-size: 16px;
  font-weight: 600;
  opacity: 0.95;
  margin-bottom: 8px;
  text-align: center;
}
.type-tables {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}
.type-table {
  flex: 1;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 4px;
  padding: 6px;
  min-height: 60px;
  min-width: 80px;
}
.table-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2px;
}
.data-cell {
  width: 16px;
  height: 8px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 2px;
  border: 1px solid rgba(255, 255, 255, 0.1);
}
.data-cell-yellow {
  background: #fbbf24;
  border: 1px solid #f59e0b;
}
.data-cell-green {
  background: #6ee7b7;
  border: 1px solid #34d399;
}
.data-cell-mixed {
  background: linear-gradient(45deg, #fbbf24 50%, #6ee7b7 50%);
  border: 1px solid #94a3b8;
}
.data-cell-purple {
  background: #c084fc;
  border: 1px solid #a855f7;
}

.hover-box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 11;
  pointer-events: none;
}

.hover-content {
  background: #2d3748;
  color: #e2e8f0;
  padding: 12px 16px;
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
  font-family: var(--slidev-code-font-family);
  font-size: 12px;
  line-height: 1.4;
  min-width: 180px;
  border: 1px solid #4a5568;
}

.loading-text {
  color: #a0aec0;
  font-style: italic;
}

.hover-title {
  color: #48bb78;
  font-weight: 600;
  margin-bottom: 8px;
}

.hover-separator {
  height: 1px;
  background: #4a5568;
  margin-bottom: 8px;
}

.hover-description {
  color: #e2e8f0;
}

.dark .hover-content {
  background: #1a202c;
  border-color: #2d3748;
}
</style>

<!--
Let's push the topic stack again and look at how the checker works.

Our checker does not work like a traditional compiler
where you have to process everything before before you can use the information.

Instead, the checker is able to pull information on demand,
evaluating only what's required. That information is local to the checker
stored in maps or arrays internally.


But even more critically, you can ask for the types _anywhere_
in a file whenever you want. If you hover over a random node,
it'll look at just what's required to provide the hover.
We often refer to this as "helicoptering", where you can just
swoop in randomly around the file and get information.

When the code changes, we simply throw away the whole checker, and start over again.
-->

---

# How TypeScript compiles _concurrently everywhere_

<div class="compilation-phases-container">
  <div class="phase-box parse-phase">
    <h3>Parse</h3>
    <div class="phase-description">
      Source code → AST<br>
      Import resolution<br>
      Syntax errors
    </div>
    <!-- Individual files that appear and expand within the Parse phase with random delays for concurrency -->
    <div class="file-grid">
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
    </div>
  </div>
  <div class="arrow">→</div>
  <div class="phase-box bind-phase">
    <h3>Bind</h3>
    <div class="phase-description">
      Symbol creation<br>
      Scope analysis<br>
      Control flow graphs
    </div>
    <!-- Files expand in Bind phase with random delays for concurrency -->
    <div class="file-grid">
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
    </div>
  </div>
  <div class="arrow">→</div>
  <div class="phase-box check-phase">
    <h3>Check</h3>
    <div class="phase-description">
      Type checking<br>
      Reference analysis<br>
      Error detection
    </div>
    <!-- Files expand in Check phase - 4 parallel checkers as separate 2x4 grids -->
    <div v-motion v-click="1" :initial="{ opacity: 0, scale: 0.8 }" :enter="{ opacity: 1, scale: 1 }" class="checker-grid-container">
      <!-- Checker 1 (top-left): 2x4 grid -->
      <div class="checker-subgrid">
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 200 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 400 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 600 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 800 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1000 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1200 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1400 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1600 } }" class="file-box"></div>
      </div>
      <!-- Checker 2 (top-right): 2x4 grid -->
      <div class="checker-subgrid">
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 300 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 500 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 700 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 900 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1100 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1300 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1500 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1700 } }" class="file-box"></div>
      </div>
      <!-- Checker 3 (bottom-left): 2x4 grid -->
      <div class="checker-subgrid">
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 400 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 600 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 800 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1000 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1200 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1400 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1600 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1800 } }" class="file-box"></div>
      </div>
      <!-- Checker 4 (bottom-right): 2x4 grid -->
      <div class="checker-subgrid">
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 240 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 440 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 640 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 840 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1040 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1240 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1440 } }" class="file-box"></div>
        <div v-motion v-click="2" :initial="{ opacity: 0, scale: 0.3 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 1640 } }" class="file-box"></div>
      </div>
    </div>
  </div>
  <div class="arrow">→</div>
  <div class="phase-box emit-phase">
    <h3>Emit</h3>
    <div class="phase-description">
      TS → JS<br>
      Syntax downleveling<br>
      File writing
    </div>
    <!-- Files expand in Emit phase -->
    <div class="file-grid">
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
      <div class="file-box"></div>
    </div>
  </div>
</div>

<style>
.compilation-phases-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 90%;
  margin: 10% auto;
  gap: 3%;
}

.phase-box {
  width: 18%;
  height: 270px;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  position: relative;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
  padding: 15px 5px 40px 5px;
  overflow: visible;
}

.parse-phase {
  background: linear-gradient(135deg, #4f46e5, #6366f1);
  color: white;
}

.bind-phase {
  background: linear-gradient(135deg, #059669, #10b981);
  color: white;
}

.check-phase {
  background: linear-gradient(135deg, #dc2626, #ef4444);
  color: white;
}

.emit-phase {
  background: linear-gradient(135deg, #7c2d12, #ea580c);
  color: white;
}

.phase-box h3 {
  margin: 0 0 8px 0;
  font-size: 1.3rem;
  font-weight: bold;
}

.phase-description {
  text-align: center;
  font-size: 0.8rem;
  line-height: 1.3;
  opacity: 0.9;
  margin-bottom: 10px;
}

.file-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(8, 1fr);
  gap: 3px;
  align-items: center;
  width: 100%;
  height: 120px;
  margin-bottom: 15px;
  padding: 0 8px;
}

.file-box {
  background: rgba(255, 255, 255, 0.3);
  border-radius: 2px;
  height: 12px;
  width: 100%;
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.arrow {
  font-size: 2rem;
  font-weight: bold;
  color: var(--slidev-theme-primary);
  opacity: 0.7;
}

/* Dark mode adjustments */
.dark .phase-box {
  box-shadow: 0 4px 15px rgba(255,255,255,0.1);
}


.checker-grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 2px;
  width: 100%;
  height: 120px;
  margin-bottom: 15px;
  padding: 0 8px;
}

.checker-grid-container .file-box {
  height: 9px;
}

.checker-subgrid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(4, 1fr);
  gap: 3px;
  border: 2px solid rgba(255, 255, 255, 0.6);
  border-radius: 4px;
  padding: 4px;
  background: rgba(255, 255, 255, 0.05);
}
</style>

<!--
Now, because of this design, we're presented with a unique solution to our concurrent checking problem.

CLICK

Simply create more than one checker, and assign each of them a subset of the files.

They'll only pull on the minimal amount of information they need to check their subset.

There may be duplicated work if those subsets reference similar files,
but the overall effect is a net win.
 -->

---

![htop screenshot, one CPU active](/img/tsc-htop.png)

<style>
	img {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		max-width: 80%;
		max-height: 80%;
		object-fit: contain;
	}
</style>

<!-- All of this together makes the difference between using just one of your cores -->

---

![htop screenshot, all CPUs active](/img/tsgo-htop.png)

<style>
	img {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		max-width: 80%;
		max-height: 80%;
		object-fit: contain;
	}
</style>

<!-- And using all of your cores. -->

---
layout: statement
---

# Concurrency bugs?

## Shockingly few!

<!--
Shockingly, when we started adding concurrency, we had very little to fix.

Our design already had shared and immutable ASTs, as that was required to reuse
ASTs between multiple builds and while typing in the editor.

The Checker remains single-threaded. All of its state is
held internally. We just spawned more than one of them.

Emit is embarrassingly parallel, but since emit can depend on things the Checker did,
we did introduce a mutex to make emit race-free.
-->

---

```diff {5-10,17}
@@ -3033,10 +3034,8 @@ func (c *Checker) getTypeOfExpression(node *ast.Node) *Type {
 		return quickType
 	}
 	// If a type has been cached for the node, return it.
-	if node.Flags&ast.NodeFlagsTypeCached != 0 {
-		if cachedType := c.flowTypeCache[node]; cachedType != nil {
-			return cachedType
-		}
+	if cachedType := c.flowTypeCache[node]; cachedType != nil {
+		return cachedType
 	}
 	startInvocationCount := c.flowInvocationCount
@@ -3046,7 +3045,6 @@ func (c *Checker) getTypeOfExpression(node *ast.Node) *Type {
 			c.flowTypeCache = make(map[*ast.Node]*Type)
 		}
 		c.flowTypeCache[node] = t
-		node.Flags |= ast.NodeFlagsTypeCached
 	}
 	return t
 }
```

<!--
Here's one example where we did cause a race condition.

Like I said, our ASTs are supposed to be immutable after creation. But, the old codebase
broke this invariant sometimes when calculating cached information, marking a node as having
previously been visited. That's fine in JS
because only one piece of code is running at a time. But, when porting to Go, we accidentally
left some of this in place. The race detector detected that we were modifying Node flags
after the fact, so we removed that.
-->

---

```diff {5-8,10,11}
@@ -2493,11 +2508,9 @@ func (c *Checker) isReachableFlowNodeWorker(flow *ast.FlowNode, noCacheCheck boo
 		case flags&ast.FlowFlagsReduceLabel != 0:
 			// Cache is unreliable once we start adjusting labels
 			c.lastFlowNode = nil
-			data := flow.Node.AsFlowReduceLabelData()
-			saveAntecedents := data.Target.Antecedents
-			data.Target.Antecedents = data.Antecedents
+			reduceLabels = append(reduceLabels, flow.Node.AsFlowReduceLabelData())
 			result := c.isReachableFlowNodeWorker(flow.Antecedent, false /*noCacheCheck*/)
-			data.Target.Antecedents = saveAntecedents
+			reduceLabels = reduceLabels[:len(reduceLabels)-1]
 			return result
```

<!--
The race detector also caught places where we were mutating our control flow graph.
This pattern was again fine in JS, and convenient for this particular code. But, that
wouldn't fly in Go and the code was rewritten to store this information somewhere else.

We of course had more race conditions than this, and Go's race detector was critical
to tracing down these issues.
-->
