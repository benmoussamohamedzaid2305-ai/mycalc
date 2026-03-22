import streamlit as st
import math

st.set_page_config(page_title="Calculatrice de Mohamed Zaid", page_icon="🧪")

st.title("Calculatrice Scientifique")
st.write("مرحباً بك في آلتك الحاسبة !")
st.write("من صنع محمد زيد بن موسى")

# قائمة العمليات - تأكد أن الأسماء هنا هي نفسها اللي في الـ if تحت
ops = ["L'addition(+)", "Soustraction(-)", "Multiplication(*)", "Division(/)", "Sinus(sin)", "Cosinus(cos)"]
choice = st.selectbox("Choisir l'opération:", ops)

col1, col2 = st.columns(2)
with col1:
    n1 = st.number_input("Le nombre 1:", value=0.0)

# العمليات اللي كتحتاج رقم واحد فقط
if choice not in ["Sinus(sin)", "Cosinus(cos)"]:
    with col2:
        n2 = st.number_input("Le nombre 2:", value=0.0)
else:
    n2 = 0 # قيمة افتراضية باش ما يوقعش خطأ

# الحساب عند الضغط على الزر
if st.button("Le résultat"):
    res = None # كنعرفو النتيجة بـ None في الأول
    
    if choice == "L'addition(+)":
        res = n1 + n2
    elif choice == "Soustraction(-)":
        res = n1 - n2
    elif choice == "Multiplication(*)":
        res = n1 * n2
    elif choice == "Division(/)":
        if n2 != 0:
            res = n1 / n2
        else:
            st.error("Error: Division par zéro!")
    elif choice == "Sinus(sin)":
        res = math.sin(math.radians(n1))
    elif choice == "Cosinus(cos)":
        res = math.cos(math.radians(n1))

    # دابا كنطبعو النتيجة غير إيلا كانت موجودة فعلاً
    if res is not None:
        st.success(f"Le résultat est {res}")
