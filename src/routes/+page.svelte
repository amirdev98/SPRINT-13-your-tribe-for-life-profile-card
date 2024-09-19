<script>
	import { SliceZone } from '@prismicio/svelte';
	import { components } from '$lib/slices';

	export let data;
</script>

<body>
	<article>
		<SliceZone slices={data.slices} {components} />
		<header>
			<h1>{data.name}</h1>
			<p><em> Tweede jaar student Front-end Designer Developer</em></p>
			<h2>
				Klasse 1998 <br />
				Geborteplaats : Napels
			</h2>
		</header>
		<div class="skills">
			<h1>Mijn Skills</h1>
			<ul>
				<li>
					Ik spreek vloeiend Italiaans, Spaans, Frans, Nederlands, <br />
					en Engels.
				</li>

				<li>
					Nu leer ik programmeer talen zoals JavaScrip<br />
					en compilers zoals Svelte-Kit.
				</li>
			</ul>
		</div>
		<div class="hobbies">
			<h1>Mijn Hobbies</h1>
			<ul>
				<li>
					Ik houd van zingen, dansen, zeilen, reizen,<br />
					tekenen en strijden voor goede doelen zoals Rechtstaat .
				</li>
			</ul>
		</div>
		<h3>Italiaase trots</h3>
		<p>
			"Beter om op een dag als leeuw te leven, dan honderd jaar als schaap."<br />
			cit. Giovanni Falcone.<br />
			Siciliaanse rechter vermoord door de Mafia.
		</p>
	</article>
</body>

<style>
    * {
        box-sizing: border-box;
    }
		body {
        height: 100%;
        margin: 0;
        /*font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;*/
    }

    body {
        display: flex;
        justify-content: center;
        align-items: center;
        color: #143b2e;
        background-color: #d2e69c;
        padding: 1rem;
    }

    article {
        width: 100%;
        max-width: 60em;
        display: flex;
        flex-direction: column;
        align-items: center;
        background: #28b5b5;
        box-shadow: 0 0 20px 20px rgba(0, 0, 0, 0.1);
        border-radius: 2rem;
        padding: 2rem;
        margin: 2rem 0;
    }

    header {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
    }

    h1 {
        margin: 1rem 0;
        color: #002b5b;
        font-size: 2rem;
        font-family: 'Alegreya', serif;
    }
    div h1 {
        margin: 1rem 0;
        color: rgb(8, 1, 85);
        text-align: center;
				font-family: 'Alegreya', serif;
    }

    p {
        margin: 0;
        padding: 1rem;
        background: rgba(5, 79, 98, 0.5);
        text-align: center;
        border-radius: 0 0 1rem 1rem;
        width: 100%;
        font-size: 1rem;
        color: azure;
        /*font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;*/
    }

    h2 {
        color: rgb(49, 5, 54);
        font-size: 1.5rem;
    }

    h3 {
        color: rgb(49, 5, 54);
        margin-top: 2rem;
    }

    li {
        font-size: 1.25rem;
        color: rgb(45, 36, 24);
    }

    .skills, .hobbies {
        background-color: rgb(215, 207, 97);
        margin: 2rem 0;
        border-radius: 25px;
        padding: 1rem;
        box-shadow: 5px 10px 15px black;
        width: 100%;
        max-width: 40em;
				font-family: 'Alegreya', serif;
    }

    .skills {
        transform: perspective(25cm) rotateX(-18deg) rotateY(25deg);
				font-family: 'Alegreya', serif;
    }

    .hobbies {
        transform: perspective(26cm) rotateX(-16deg) rotateY(-18deg);
				font-family: 'Alegreya', serif;
    }

    ::selection {
        color: black;
        background-color: #f0eec9;
    }

    @media (max-width: 768px) {
        article {
            padding: 1rem;
            margin: 1rem 0;
        }

        h1, h2, h4 {
            font-size: 1.5rem;
        }

        li {
            font-size: 1rem;
        }

        .skills, .hobbies {
            transform: none;
            margin: 1rem 0;
						font-family: 'Alegreya', serif;
        }
    }
</style>
