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
        "A",
        "B",
        "C",
        "D",
        "E",
        "F",
        "G",
        "H",
        "I",
        "J",
        "K",
        "L",
        "M",
        "N",
        "O",
        "P",
        "Q",
        "R",
        "S",
        "T",
        "U",
        "V",
        "W",
        "X",
        "Y",
        "Z",
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
        ":",
        " ",
    ];
    const random_num = () => {
        let num = Math.floor(Math.random() * 100);
        if (num > 0) {
            return num;
        } else {
            return random_num();
        }
    };
    function crypt(msg) {
        console.clear();
        // @ts-ignore

        let encrypted = "";
        let arr = msg.split("");
        console.log(arr);
        arr.map((letter) => {
            let num = random_num();
            let index = alp.indexOf(letter) + 1;
            encrypted += `${index * num}-${num}`;
            if (msg.indexOf(letter) < msg.length - 1)
            {
                encrypted+="-"
            }
        });

        if (encrypted.includes("NaN") || encrypted.includes("undefined")) {
            encrypted = "";
            crypt(msg)
            return
        }

        // @ts-ignore
        document.getElementById("output").value = encrypted;
    }
    function encrypt(e) {
        console.clear();
        e.preventDefault();
        // @ts-ignore
        crypt(document.getElementById("input").value)
    }
    function decrypt(e) {
        e.preventDefault();
        // @ts-ignore
        let message = document.getElementById("input").value;

        let decrypted = "";
        let arr = message.split("-");

        arr = arr.filter((letter) => {
            return letter !== ""
        })

        console.log(arr);
        for (let i = 0; i < arr.length; i += 2) {
            let index = parseInt(arr[i]);
            let num = parseInt(arr[i + 1]);
            decrypted += alp[index / num - 1];
        }

        if (decrypted.includes("NaN") || decrypted.includes("undefined")) {
            decrypted = "";
            alert("Invalid Input, there are double spaces or the message was encrypted twice.")
        }

        // @ts-ignore
        document.getElementById("output").value = decrypted;
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
