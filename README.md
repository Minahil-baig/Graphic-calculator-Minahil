
import streamlit as st

st.set_page_config(page_title="Calculator", layout="centered")
st.title(" Graphic Calculator")

if "expression" not in st.session_state:
    st.session_state.expression = ""

expression = st.text_input("Type number or use buttons:", value=st.session_state.expression)

if expression != st.session_state.expression:
    if expression.endswith("="):
        try:
            expression = str(eval(expression[:-1]))
        except:
            expression = "Error"
    st.session_state.expression = expression

st.code(st.session_state.expression, language="")

def button_click(value):
    if value == "C":
        st.session_state.expression = ""
    elif value == "=":
        try:
            st.session_state.expression = str(eval(st.session_state.expression))
        except:
            st.session_state.expression = "Error"
    else:
        st.session_state.expression += value

buttons = [
    ["7", "8", "9", "÷"],
    ["4", "5", "6", "×"],
    ["1", "2", "3", "-\u00A0"],
    ["C", "0", "=", "+\u00A0"]

]

for row in buttons:
    cols = st.columns(len(row))
    for i, label in enumerate(row):
        cols[i].button(f"{label}", on_click=button_click, args=(label,))# Graphic-calculator-Minahil


