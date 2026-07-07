(function () {
  "use strict";

  /* ======================================================
     DATA — Wilayas & Communes (Algeria)
     NOTE: communes below cover the major/well-known wilayas
     with a curated list. Wilayas without a curated list fall
     back to a single generic "مركز الولاية" entry so the field
     always works — replace WILAYA_COMMUNES with the full
     official 1541-commune dataset before production use.
     ====================================================== */
  var WILAYAS = [
    "أدرار", "الشلف", "الأغواط", "أم البواقي", "باتنة", "بجاية", "بسكرة", "بشار",
    "البليدة", "البويرة", "تمنراست", "تبسة", "تلمسان", "تيارت", "تيزي وزو", "الجزائر",
    "الجلفة", "جيجل", "سطيف", "سعيدة", "سكيكدة", "سيدي بلعباس", "عنابة", "قالمة",
    "قسنطينة", "المدية", "مستغانم", "المسيلة", "معسكر", "ورقلة", "وهران", "البيض",
    "إليزي", "برج بوعريريج", "بومرداس", "الطارف", "تندوف", "تيسمسيلت", "الوادي",
    "خنشلة", "سوق أهراس", "تيبازة", "ميلة", "عين الدفلى", "النعامة", "عين تموشنت",
    "غرداية", "غليزان", "تيميمون", "برج باجي مختار", "أولاد جلال", "بني عباس",
    "عين صالح", "عين قزام", "تقرت", "جانت", "المغير", "المنيعة"
  ];

  var WILAYA_COMMUNES = {
    "الجزائر": ["الجزائر الوسطى", "باب الوادي", "حسين داي", "بئر مراد رايس", "الحراش", "درارية", "بئر خادم", "الدار البيضاء"],
    "وهران": ["وهران", "السانيا", "بئر الجير", "عين الترك", "أرزيو", "بطيوة", "المرسى الكبير"],
    "قسنطينة": ["قسنطينة", "الخروب", "عين عبيد", "حامة بوزيان", "ديدوش مراد", "زيغود يوسف"],
    "البليدة": ["البليدة", "بوفاريك", "الأربعاء", "موزاية", "بوعينان", "العفرون"],
    "تيزي وزو": ["تيزي وزو", "عزازقة", "الأربعاء نايت إيراثن", "بوغني", "درعن", "تيقزيرت"],
    "بجاية": ["بجاية", "أقبو", "أميزور", "سيدي عيش", "القصر", "تيشي"],
    "سطيف": ["سطيف", "العلمة", "عين ولمان", "بابور", "بئر العرش", "عين أزال"],
    "باتنة": ["باتنة", "بريكة", "تازولت", "مروانة", "عين التوتة", "أريس"],
    "عنابة": ["عنابة", "الحجار", "البوني", "سرايدي", "برحال"],
    "تلمسان": ["تلمسان", "مغنية", "ندرومة", "الرمشي", "شتوان", "هنين"],
    "تيارت": ["تيارت", "فرندة", "السوقر", "مهدية", "عين الذهب"],
    "الجلفة": ["الجلفة", "عين وسارة", "حاسي بحبح", "مسعد", "دار الشيوخ"],
    "ورقلة": ["ورقلة", "حاسي مسعود", "تقرت", "الرويسات", "النزلة"],
    "سيدي بلعباس": ["سيدي بلعباس", "تلاغ", "سفيزف", "المحمدية"],
    "مستغانم": ["مستغانم", "عين تادلس", "حاسي ماماش", "بوقيراط"],
    "سكيكدة": ["سكيكدة", "عزابة", "القل", "رمضان جمال"],
    "المدية": ["المدية", "قصر البخاري", "برواقية", "تابلاط"],
    "بومرداس": ["بومرداس", "بودواو", "برج منايل", "الثنية", "دلس"],
    "قالمة": ["قالمة", "بوشقوف", "هيليوبوليس", "وادي الزناتي"],
    "بشار": ["بشار", "بني ونيف", "القنادسة", "تاغيت"],
    "غرداية": ["غرداية", "متليلي", "بريان", "المنصورة"]
  };

  function communesFor(wilayaName) {
    return WILAYA_COMMUNES[wilayaName] || ["مركز " + wilayaName];
  }

  /* ======================================================
     HEADER — scroll blur + hide on scroll down
     ====================================================== */
  var header = document.getElementById("siteHeader");
  var stickyCta = document.getElementById("stickyCta");
  var lastScrollY = window.scrollY;

  function onScroll() {
    var y = window.scrollY;

    if (y > 12) header.classList.add("is-scrolled");
    else header.classList.remove("is-scrolled");

    if (y > lastScrollY && y > 160) header.classList.add("is-hidden");
    else header.classList.remove("is-hidden");

    if (stickyCta) {
      if (y > 320) stickyCta.classList.add("is-visible");
      else stickyCta.classList.remove("is-visible");
    }

    lastScrollY = y;
  }
  window.addEventListener("scroll", onScroll, { passive: true });

  /* ======================================================
     GALLERY — desktop thumbnails + mobile swipe slider
     ====================================================== */
  var mainImage = document.getElementById("galleryMainImage");
  var thumbs = document.querySelectorAll(".thumb");

  thumbs.forEach(function (thumb) {
    thumb.addEventListener("click", function () {
      var full = thumb.getAttribute("data-full");
      if (mainImage.getAttribute("src") === full) return;
      mainImage.style.opacity = "0";
      window.setTimeout(function () {
        mainImage.setAttribute("src", full);
        mainImage.style.opacity = "1";
      }, 140);
      thumbs.forEach(function (t) { t.classList.remove("is-active"); });
      thumb.classList.add("is-active");
    });
  });
  mainImage.style.transition = "opacity 0.15s ease";

  var slider = document.getElementById("gallerySlider");
  var dots = document.querySelectorAll("#galleryDots .dot");
  if (slider && dots.length) {
    slider.addEventListener("scroll", function () {
      var index = Math.round(slider.scrollLeft / slider.clientWidth);
      dots.forEach(function (d, i) { d.classList.toggle("is-active", i === index); });
    }, { passive: true });
  }

  /* ======================================================
     SCROLL REVEAL — IntersectionObserver fade-in-up
     ====================================================== */
  var revealEls = document.querySelectorAll(".reveal");
  if ("IntersectionObserver" in window) {
    var revealObserver = new IntersectionObserver(function (entries) {
      entries.forEach(function (entry) {
        if (entry.isIntersecting) {
          entry.target.classList.add("is-visible");
          revealObserver.unobserve(entry.target);
        }
      });
    }, { threshold: 0.15 });
    revealEls.forEach(function (el) { revealObserver.observe(el); });
  } else {
    revealEls.forEach(function (el) { el.classList.add("is-visible"); });
  }

  /* ======================================================
     ACCORDION
     ====================================================== */
  document.querySelectorAll(".accordion-trigger").forEach(function (trigger) {
    trigger.addEventListener("click", function () {
      var item = trigger.closest(".accordion-item");
      var panel = item.querySelector(".accordion-panel");
      var isOpen = item.classList.contains("is-open");

      document.querySelectorAll(".accordion-item").forEach(function (other) {
        other.classList.remove("is-open");
        other.querySelector(".accordion-panel").style.maxHeight = null;
      });

      if (!isOpen) {
        item.classList.add("is-open");
        panel.style.maxHeight = panel.scrollHeight + "px";
      }
    });
  });

  /* ======================================================
     ORDER ENGINE
     ====================================================== */
  var UNIT_PRICE = 8750;

  var state = {
    quantity: 1,
    deliveryPrice: 600,
    color: "ذهبي"
  };

  var priceNewEl = document.getElementById("priceNew");
  var summaryUnitPriceEl = document.getElementById("summaryUnitPrice");
  var stickyPriceEl = document.getElementById("stickyPrice");
  var orderTotalEl = document.getElementById("orderTotal");
  var qtyInput = document.getElementById("qtyInput");

  function formatDA(n) {
    return n.toLocaleString("fr-FR").replace(/,/g, ".") + " د.ج";
  }

  function renderTotals() {
    var subtotal = UNIT_PRICE * state.quantity;
    var total = subtotal + state.deliveryPrice;
    orderTotalEl.textContent = formatDA(total);
  }

  [priceNewEl, summaryUnitPriceEl, stickyPriceEl].forEach(function (el) {
    if (el) el.textContent = formatDA(UNIT_PRICE);
  });
  renderTotals();

  /* Color / variant selection */
  document.getElementById("colorGroup").addEventListener("click", function (e) {
    var btn = e.target.closest(".variant-btn");
    if (!btn) return;
    document.querySelectorAll("#colorGroup .variant-btn").forEach(function (b) { b.classList.remove("is-active"); });
    btn.classList.add("is-active");
    state.color = btn.getAttribute("data-value");
  });

  /* Quantity stepper */
  document.getElementById("qtyMinus").addEventListener("click", function () {
    if (state.quantity > 1) {
      state.quantity -= 1;
      qtyInput.value = state.quantity;
      renderTotals();
    }
  });
  document.getElementById("qtyPlus").addEventListener("click", function () {
    if (state.quantity < 10) {
      state.quantity += 1;
      qtyInput.value = state.quantity;
      renderTotals();
    }
  });

  /* Delivery type */
  document.getElementById("deliveryGroup").addEventListener("click", function (e) {
    var card = e.target.closest(".delivery-card");
    if (!card) return;
    document.querySelectorAll(".delivery-card").forEach(function (c) { c.classList.remove("is-active"); });
    card.classList.add("is-active");
    state.deliveryPrice = parseInt(card.getAttribute("data-price"), 10);
    renderTotals();
  });

  /* Wilaya -> Commune */
  var wilayaSelect = document.getElementById("wilaya");
  var communeSelect = document.getElementById("commune");

  WILAYAS.forEach(function (name, i) {
    var opt = document.createElement("option");
    opt.value = name;
    opt.textContent = (i + 1).toString().padStart(2, "0") + " - " + name;
    wilayaSelect.appendChild(opt);
  });

  wilayaSelect.addEventListener("change", function () {
    var communes = communesFor(wilayaSelect.value);
    communeSelect.innerHTML = "";
    var placeholder = document.createElement("option");
    placeholder.value = "";
    placeholder.disabled = true;
    placeholder.selected = true;
    placeholder.textContent = "اختر البلدية";
    communeSelect.appendChild(placeholder);

    communes.forEach(function (c) {
      var opt = document.createElement("option");
      opt.value = c;
      opt.textContent = c;
      communeSelect.appendChild(opt);
    });
    communeSelect.disabled = false;
  });

  /* Phone field: digits only */
  var phoneInput = document.getElementById("phone");
  var phoneError = document.getElementById("phoneError");
  phoneInput.addEventListener("input", function () {
    phoneInput.value = phoneInput.value.replace(/\D/g, "").slice(0, 9);
    phoneError.textContent = "";
  });

  function isValidPhone(value) {
    return /^(5|6|7)\d{8}$/.test(value);
  }

  /* ======================================================
     ORDER SUBMIT -> OTP FLOW
     ====================================================== */
  var orderForm = document.getElementById("orderForm");
  var submitBtn = document.getElementById("submitBtn");
  var otpOverlay = document.getElementById("otpOverlay");
  var otpClose = document.getElementById("otpClose");
  var otpInputs = document.querySelectorAll(".otp-box");
  var otpError = document.getElementById("otpError");
  var otpPhoneDisplay = document.getElementById("otpPhoneDisplay");
  var otpCountdownEl = document.getElementById("otpCountdown");
  var otpResendBtn = document.getElementById("otpResend");
  var successToast = document.getElementById("successToast");

  var countdownTimer = null;
  var countdownSeconds = 59;

  orderForm.addEventListener("submit", function (e) {
    e.preventDefault();

    var fullName = document.getElementById("fullName").value.trim();
    var phone = phoneInput.value.trim();
    var wilaya = wilayaSelect.value;
    var commune = communeSelect.value;

    if (!fullName) {
      document.getElementById("fullName").focus();
      return;
    }
    if (!isValidPhone(phone)) {
      phoneError.textContent = "رقم الهاتف غير صحيح، تأكد من إدخال 9 أرقام تبدأ بـ 5 أو 6 أو 7";
      phoneInput.focus();
      return;
    }
    if (!wilaya) {
      wilayaSelect.focus();
      return;
    }
    if (!commune) {
      communeSelect.focus();
      return;
    }

    submitBtn.classList.add("is-loading");
    submitBtn.disabled = true;

    /*
      Integration point: send order to backend (e.g. Youzin's
      order-create endpoint) here via fetch(), then open the
      OTP modal once the server responds with pending_otp status.
      Example:
      fetch('/api/orders/create.php', { method: 'POST', body: ... })
        .then(res => res.json())
        .then(data => { if (data.status === 'pending_otp') openOtpModal(phone); });
    */
    window.setTimeout(function () {
      submitBtn.classList.remove("is-loading");
      submitBtn.disabled = false;
      openOtpModal(phone);
    }, 1100);
  });

  function openOtpModal(phone) {
    otpPhoneDisplay.textContent = "+213 " + phone;
    otpOverlay.classList.add("is-open");
    otpInputs.forEach(function (input) { input.value = ""; input.classList.remove("has-error"); });
    otpError.textContent = "";
    otpInputs[0].focus();
    startCountdown();
  }

  function closeOtpModal() {
    otpOverlay.classList.remove("is-open");
    clearInterval(countdownTimer);
  }

  otpClose.addEventListener("click", closeOtpModal);
  otpOverlay.addEventListener("click", function (e) {
    if (e.target === otpOverlay) closeOtpModal();
  });

  function startCountdown() {
    countdownSeconds = 59;
    otpResendBtn.disabled = true;
    updateCountdownDisplay();
    clearInterval(countdownTimer);
    countdownTimer = window.setInterval(function () {
      countdownSeconds -= 1;
      updateCountdownDisplay();
      if (countdownSeconds <= 0) {
        clearInterval(countdownTimer);
        otpResendBtn.disabled = false;
      }
    }, 1000);
  }

  function updateCountdownDisplay() {
    var s = Math.max(countdownSeconds, 0);
    otpCountdownEl.textContent = "00:" + (s < 10 ? "0" + s : s);
  }

  otpResendBtn.addEventListener("click", function () {
    if (otpResendBtn.disabled) return;
    otpInputs.forEach(function (input) { input.value = ""; });
    otpError.textContent = "";
    otpInputs[0].focus();
    startCountdown();
    /* Integration point: call backend to resend a new OTP code */
  });

  /* OTP boxes: auto-advance + auto-submit on last digit */
  otpInputs.forEach(function (input, index) {
    input.addEventListener("input", function () {
      input.value = input.value.replace(/\D/g, "").slice(0, 1);
      input.classList.remove("has-error");
      otpError.textContent = "";

      if (input.value && index < otpInputs.length - 1) {
        otpInputs[index + 1].focus();
      }

      var allFilled = Array.prototype.every.call(otpInputs, function (i) { return i.value.length === 1; });
      if (allFilled) {
        verifyOtp();
      }
    });

    input.addEventListener("keydown", function (e) {
      if (e.key === "Backspace" && !input.value && index > 0) {
        otpInputs[index - 1].focus();
      }
    });

    input.addEventListener("paste", function (e) {
      var pasted = (e.clipboardData || window.clipboardData).getData("text").replace(/\D/g, "");
      if (!pasted) return;
      e.preventDefault();
      pasted.split("").slice(0, otpInputs.length).forEach(function (digit, i) {
        otpInputs[i].value = digit;
      });
      var lastIndex = Math.min(pasted.length, otpInputs.length) - 1;
      if (lastIndex >= 0) otpInputs[lastIndex].focus();
      var allFilled = Array.prototype.every.call(otpInputs, function (i) { return i.value.length === 1; });
      if (allFilled) verifyOtp();
    });
  });

  function verifyOtp() {
    var code = Array.prototype.map.call(otpInputs, function (i) { return i.value; }).join("");

    /*
      Integration point: replace this simulated check with a real
      call to verify_otp.php, e.g.:
      fetch('/api/verify_otp.php', { method: 'POST', body: JSON.stringify({ code }) })
        .then(res => res.json())
        .then(data => data.valid ? onOtpSuccess() : onOtpFailure());
    */
    var simulatedValid = code.length === 4;

    if (simulatedValid) {
      onOtpSuccess();
    } else {
      onOtpFailure();
    }
  }

  function onOtpSuccess() {
    clearInterval(countdownTimer);
    closeOtpModal();
    orderForm.reset();
    state.quantity = 1;
    qtyInput.value = 1;
    renderTotals();
    showToast();
    /* Integration point: fire Facebook Pixel Purchase event here, post-confirmation only */
  }

  function onOtpFailure() {
    otpError.textContent = "الرمز غير صحيح، حاول مرة أخرى";
    otpInputs.forEach(function (input) { input.classList.add("has-error"); input.value = ""; });
    otpInputs[0].focus();
  }

  function showToast() {
    successToast.classList.add("is-visible");
    window.setTimeout(function () { successToast.classList.remove("is-visible"); }, 3800);
  }

})();
