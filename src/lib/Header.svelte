<script>
    // 0-57-267-89-0-25-45-15-0-34-3-1-279-93-0-72
    const alp = [
        "a",
        "b",
        "c",
        "d",
        "e",
        "f",
        "g",
        "h",
        "i",
        "j",
        "k",
        "l",
        "m",
        "n",
        "o",
        "p",
        "q",
        "r",
        "s",
        "t",
        "u",
        "v",
        "w",
        "x",
        "y",
        "z",
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7",
        "8",
        "9",
        "!",
        ",",
        ".",
        "?",
        "-",
        "_",
        "+",
        "=",
        "/",
        "\\",
        "*",
        "&",
        "^",
        "%",
        "$",
        "#",
        "@",
        "~",
        "`",
        "|",
        '"',
        "'",
        "<",
        ">",
        " ",
    ];
    function encrypt(e) {
        e.preventDefault();
        // @ts-ignore
        let input = document.getElementById("input").value;

        input = input.toLowerCase();

        input = input.split("");

        let output = [];

        input.map((l) => {
            let num = Math.floor(Math.random() * 100);
            output.push(alp.indexOf(l) * num);
            output.push(num);
        });

        let res = "";

        for (let i = 0; i < output.length; i++) {
            res += output[i];
            if (i !== output.length - 1) {
                res += "-";
            }
        }

        // @ts-ignore
        document.getElementById("output").value = res;
    }
    function decrypt(e) {
        e.preventDefault();
        // @ts-ignore
        let input = document.getElementById("input").value;

        input = input.split("-");

        let output = [];

        for (let i = 0; i < input.length; i += 2) {
            output.push(alp[input[i] / input[i + 1]]);
        }
        let res = "";
        for (let i = 0; i < output.length; i++) {
            if (output[i] === undefined) {
                alert("Invalid Input, make sure that there aren't any double hyphens and that the input hasn't been encrypted twice.")
                res = ""
                break;
            }
            res += output[i];
        }

        // @ts-ignore
        document.getElementById("output").value = res;
    }
</script>

<div>
    <form id="form" action="">
        <div class="flex col center">
            <label class="text-white h1" for="input">INPUT</label>
            <textarea
                name="input"
                id="input"
                cols="60"
                rows="15"
                autocomplete="on"
                required
                wrap="hard"
            />
            <div class="buttons flex row space-between">
                <button class="text-white" on:click={encrypt}>ENCRYPT</button>
                <button class="text-white" on:click={decrypt}>DECRYPT</button>
            </div>
            <textarea
            name="output"
            id="output"
            cols="60"
            rows="15"
            autocomplete="on"
            readonly
            />
            <label class="text-white h1" for="output">OUTPUT</label>
        </div>
    </form>
</div>

<style>
    textarea {
        resize: none;
        border: none;
        border-radius: 5px;
        box-shadow: 14px 14px 30px 0px rgba(0, 0, 0, 0.1);
        transition: scale 0.3s;
        margin-block: 5px;
        background-color: #edddd4;
        padding: 10px;
        width: 100%;
        outline: none;
    }
    #input:focus {
        scale: 1.01;
        box-shadow: 14px 14px 30px 0px rgba(0, 0, 0, 0.3);
    }
    button {
        border: none;
        border-radius: 5px;
        padding: 5px;
        background-color: #cd6e10;
        font-weight: 600;
        width: 10rem;
        height: 3rem;
        transition: scale 0.1s;
        font-size: 1.09em;
    }
    .buttons {
        width: 100%;
        padding-inline: 0px;
        margin-block: 10px;
    }
    button:hover {
        scale: 1.01;
        box-shadow: 14px 14px 30px 0px rgba(0, 0, 0, 0.3);
    }
    button:active {
        scale: 0.99;
        box-shadow: 14px 14px 30px 0px rgba(0, 0, 0, 0.1);
    }
    @media screen and (max-width: 600px) {
        textarea {
            max-width: 300px;
            height: 250px;
            width: 100%;
        }
        button {
            max-width: 100px;
        }
    }
</style>
