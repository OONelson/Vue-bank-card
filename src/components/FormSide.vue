<template>
	<main class="container">
		<div v-if="display">
			<img
				src="../assets/bg-main-desktop.png"
				class="background"
				alt="gradient background"
			/>
			<img
				src="../assets/bg-card-front.png"
				class="cardFront absolute"
				alt="card front"
			/>
			<img
				src="../assets/bg-card-back.png"
				class="cardBack absolute"
				alt="card back"
			/>
			<img
				src="../assets/card-logo.svg"
				class="cardLogo absolute"
				alt="card logo"
			/>
		</div>
		<div
			class="cardDetails"
			v-if="display"
		>
			<p class="cardNumber absolute">{{ cardNumber }}</p>

			<span class="cardName absolute"> {{ cardName }} </span>
			<div class="exp absolute">
				<span class="cardMonth"> {{ cardMonth }} / </span>
				<span class="cardYear"> {{ cardYear }} </span>
			</div>
			<span class="cardCvc absolute"> {{ cardCvc }} </span>
		</div>

		<form
			class="form"
			@submit.prevent="submitForm"
			v-if="display"
		>
			<div class="divname column">
				<label>cardholder name</label>

				<input
					type="text"
					class="name input"
					placeholder="e.g Jane Appleaseed"
					v-model="cardName"
				/>
			</div>

			<div class="divnumber column">
				<label>card number</label>

				<input
					type="number"
					class="number input"
					placeholder="e.g 1234 5678 9053 0000"
					v-model="cardNumber"
				/>
			</div>

			<div class="group">
				<div class="divdate column">
					<!-- <div class="column"> -->
					<label>exp. date(mm/yy)</label>
					<div class="row">
						<input
							type="month-local"
							class="month numbers"
							placeholder="MM"
							v-model="cardMonth"
						/>
						<!-- </div> -->

						<input
							type="date-local"
							class="year numbers"
							placeholder="YY"
							v-model="cardYear"
						/>
					</div>
				</div>

				<div class="divcvc column">
					<label>cvc</label>
					<span class="spanCvc red absolute"></span>
					<input
						type="number"
						class="cvc"
						placeholder="e.g 123"
						v-model="cardCvc"
					/>
				</div>
			</div>
			<button
				class="submit"
				@submit.prevent="submitForm"
			>
				submit
			</button>
		</form>

		<div
			class="success"
			v-if="formSubmitted && isValid"
		>
			<img
				src="../assets/icon-complete.svg"
				class="mark"
				alt="tick"
			/>
			<h3>thank you!</h3>
			<p>We've added your card details</p>
			<button>Continue</button>
		</div>
	</main>
</template>

<script>
export default {
	data() {
		return {
			cardName: '',
			cardNumber: '',
			cardMonth: '',
			cardYear: '',
			cardCvc: '',
			formSubmitted: false,
			isValid: false,
			display: true
		};
	},
	computed: {
		isCardNameValid() {
			return /^[a-zA-Z\s]+$/.test(this.cardname);
		},
		isCardNumberValid() {
			return /^\d{16}$/.test(this.cardNumber);
		},
		isCardMonthValid() {
			return /^(0[1-9]|1[0-2])$/.test(this.cardMonth);
		},
		isCardYearValid() {
			return /^\d{2}$/.test(this.cardYear);
		},
		isCardCvcValid() {
			return /^\d{3}$/.test(this.cardCvc);
		}
	},
	watch: {
		isCardNameValid() {
			this.updateValidity();
			this.cardName.toUpperCase();
		},
		isCardNumberValid() {
			this.updateValidity();
		},
		isCardMonthValid() {
			this.updateValidity();
		},
		isCardYearValid() {
			this.updateValidity();
		},
		isCardCvcValid() {
			this.updateValidity();
		}
	},
	methods: {
		updateValidity() {
			this.isValid =
				this.isCardNameValid &&
				this.isCardNumberValid &&
				this.isCardMonthValid &&
				this.isCardYearValid &&
				this.isCardCvcValid;
		},
		submitForm() {
			if (this.isValid) {
				this.isValid = true;
				this.formSubmitted = true;
				this.display = false;
			} else {
				alert('Invalid Format');
			}
		}
	}
};
</script>

<style>
form {
	padding: 1.5rem;
	height: max-content;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	margin-right: 15rem;
	overflow: hidden;
	color: hsl(278, 68%, 11%);
}
input {
	margin-bottom: 0.5rem;
	border-radius: 0.5rem;
	border: 1px solid hsl(270, 3%, 87%);
	color: hsl(278, 68%, 11%);
}
input:active {
	border: none;
	border: 1px solid
		linear-gradient(to bottom right, hsl(249, 88%, 62%), hsl(278, 94%, 30%));
}
input:focus {
	border: 1px solid
		linear-gradient(to bottom right, hsl(249, 88%, 62%), hsl(278, 94%, 30%));
}
div {
	display: flex;
}
button {
	padding: 0.5rem 6.8rem;
	margin-top: 1.5rem;
	color: #fff;
	border-radius: 0.5rem;
	background-color: hsl(278, 68%, 11%);
	border: none;
	cursor: pointer;
	transition: all 0.3s linear;
}
button:hover {
	box-shadow: 0 0.5rem 1rem rgb(0, 0, 0, 0.6);
	transform: translateY(-0.7rem);
}
button:active {
	box-shadow: 0 0.5rem 0.5rem rgb(0, 0, 0, 0.6);
	transform: translateY(0rem);
}

.background {
	width: 30%;
	height: 100%;
}
.absolute {
	position: absolute;
	color: #fff;
}
.cardFront {
	width: 30%;
	height: 30%;
	top: 20%;
	left: 15%;
	/* transform: translate(-50%, -50%); */
}
.cardBack {
	width: 30%;
	height: 30%;
	top: 55%;
	left: 20%;
}
.cardLogo {
	width: 7%;
	height: 8%;
	top: 22%;
	left: 16%;
}
.cardName {
	top: 45%;
	left: 18%;
}
.cardNumber {
	top: 30%;
	left: 18%;
	font-size: 1.8rem;
}
.exp {
	top: 45%;
	left: 38%;
}
.cardCvc {
	top: 68%;
	left: 44%;
}
.container {
	position: relative;
	width: 100vw;
	height: 100vh;
	overflow: hidden;
	display: flex;
	justify-content: space-between;
	align-items: center;
}
.input {
	width: 15rem;
	padding: 0.4rem;
}
.column {
	flex-direction: column;
}
.row {
	flex-direction: row;
}
.group input {
	padding: 0.4rem 0.2rem;
}
.cvc {
	width: 5.5rem;
}
.numbers {
	width: 3.5rem;
	margin-right: 1rem;
}
.success {
	width: 40rem;
	height: max-content;
	border-radius: 0.3rem;
	padding: 2rem;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	color: hsl(278, 68%, 11%);
	text-align: center;
	transition: all 0.5s linear;
}
.success img {
	padding: 1rem 0 2rem 0;
}
.success h3 {
	font-size: 2rem;
}
.success p {
	color: hsl(270, 3%, 87%);
}

@media screen and (max-width: 425px) {
	.container {
		flex-direction: column;
		justify-content: center;
		padding-top: 0;
		height: 100vh;
		/* position: relative; */
	}
	form {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translateX(-50%);
	}
	.background {
		width: 100vw;
		height: 40vh;
		position: absolute;
		inset: 0;
	}
	.cardFront {
		top: 1%;
		left: 5%;
		height: 23vh;
		width: 70vw;
	}
	.cardBack {
		top: 28%;
		left: 15%;
		height: 23vh;
		width: 70vw;
	}
	.cardLogo {
		width: 2.5rem;
		height: 1rem;
		top: 2%;
		left: 6%;
	}
	.cardNumber {
		top: 2%;
		left: 10%;
		font-size: 1.5rem;
	}
	.cardName {
		top: 17%;
		left: 6%;
		font-size: 0.8rem;
		text-transform: uppercase;
	}
	.exp {
		top: 17%;
		left: 63%;
	}
	.cardCvc {
		top: 37%;
		left: 63%;
	}
}
@media screen and (max-width: 425px) {
	.cardNumber {
		font-size: 0.8rem;
	}
	.exp {
		left: 60%;
	}
}
@keyframes animate {
	0% {
		opacity: 0;
		transform: translateY(1rem);
	}
	20% {
		transform: translateY(-1rem);
		opacity: 0.8;
	}
	60% {
		transform: translateY(-2rem);
		opacity: 1;
	}
	100% {
		transform: translateY(0);
		opacity: 1;
	}
}
</style>
