
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Typewriting Effect</title>
    <style>
        :root {
            --link-hover-color: #0074ff; /* Blue */
            --image-outline-color: #0045ff; /* Blue */
            --header-active-background-color: rgba(0, 76, 255, 0.55); /* Blue */
        }

        .typewrite {
            color: var(--link-hover-color);
            filter: drop-shadow(0 0 2px var(--image-outline-color)) drop-shadow(0 0 20px var(--image-outline-color));
            font-size: 1.5em;
        }

        .typewrite > .wrap {
            border-right: 0.06em solid var(--header-active-background-color);
        }
    </style>
</head>
<body>
    <h1>
        <span class="typewrite" data-period="2000" data-type='["Welcome to CAP_PRIME.","Made by CAP.","I Made this for BlueSpace."]'>
            <span class="wrap"></span>
        </span>
    </h1>

    <script>
        class TxtType {
            constructor(el, toRotate, period) {
                this.toRotate = toRotate;
                this.el = el;
                this.loopNum = 0;
                this.period = parseInt(period, 10) || 2000;
                this.txt = '';
                this.tick();
                this.isDeleting = false;
            }

            tick() {
                const i = this.loopNum % this.toRotate.length;
                const fullTxt = this.toRotate[i];

                if (this.isDeleting) {
                    this.txt = fullTxt.substring(0, this.txt.length - 1);
                } else {
                    this.txt = fullTxt.substring(0, this.txt.length + 1);
                }

                this.el.innerHTML = `<span class="wrap">${this.txt}</span>`;

                let delta = 200 - Math.random() * 100;

                if (this.isDeleting) {
                    delta /= 2;
                }

                if (!this.isDeleting && this.txt === fullTxt) {
                    delta = this.period;
                    this.isDeleting = true;
                } else if (this.isDeleting && this.txt === '') {
                    this.isDeleting = false;
                    this.loopNum++;
                    delta = 500;
                }

                setTimeout(() => this.tick(), delta);
            }
        }

        document.addEventListener('DOMContentLoaded', function () {
            const elements = document.getElementsByClassName('typewrite');
            for (let i = 0; i < elements.length; i++) {
                const toRotate = elements[i].getAttribute('data-type');
                const period = elements[i].getAttribute('data-period');
                if (toRotate) {
                    new TxtType(elements[i], JSON.parse(toRotate), period);
                }
            }
        });
        
  
    </script>
