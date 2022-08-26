<!DOCTYPE html>
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        <style>
            body{
                margin-right: 10px;
                max-height: fit-content;
            }

            .box{
                min-width: 140px;
                max-width: 100%;
                height: 100%;
                min-height: 100px;

                margin: 5px;

                border-width: 5px;
                border-color: black;
                border-style: solid;
                border-radius: 15px;
            }
            .box .inn{
                display: flex;
                width: 100%;

                justify-content: center;
            }
            .box .inn2{
                display: flex;
                flex-wrap: wrap;
                width: 100%;

                justify-content: center;
            }
            .box div[contenteditable]{
                margin-top: 0;
                margin-bottom: auto;

                background: rgb(226, 226, 226);
                color: black;

                border-top-left-radius: 5px;
                border: 0;
                outline: 0;

                width: 100%;
                height: 15px;
                resize: none;
                min-height: 18px;
                max-height: 50px;

                transition: 0.25s;
            }
            .box div[contenteditable]:hover{
                background: rgb(68, 68, 68);
                color: white;
            }
            .box div[contenteditable]:focus{
                background: rgb(68, 68, 68);
                color: white;
            }
            .box Button{
                border-radius: 5px;
                border-color: black;

                background: black;
                color: white;
                cursor: pointer;
                transition: 0.25s;
            }
            .box Button:hover{
                border-color: white;
                background: white;
                color: black;
            }
            .notes{
                display: block;
                position: relative;

                outline: none;
                resize: none;
                font-size: large;
                
                background-color: rgb(40, 40, 40);
                color: white;

                border-radius: 10px;
                /*right: 2.5px;*/

                width: 100%;
                min-height: 80px;

            }
            .notes .t{
                outline: none;
                resize: none;
                font-size: large;

                padding: 10px;
            }

        </style>
    </head>
    <body spellcheck="false" oncontextmenu="return false">
        <div class="box">
            <div class="inn">
                <div contenteditable="true"></div>
                <Button id="0" onmousedown="MakeBox(event.button, this.id)"></Button>
            </div>
            <div class="inn2"></div>
        </div>
        <div class="notes" oninput='this.style.height = "";this.style.height = this.scrollHeight + "px"'>
            <div class="t" contenteditable="true">

            </div>
        </div>

        <section>
            <script>
                //go through all ids
                function Ids(){
                    var ID = [];
                    $("*").each(function() {
                        if (this.id) {
                            ID.push(this.id);
                        }
                    });
                    return ID;
                }
                //find largest id
                function LargestId(){
                    CurLargest = 0;
                    for (let index = 0; index < Ids().length; index++) {
                        const Elem = parseInt(Ids()[index]);
                        if(Elem > CurLargest){
                            CurLargest = Elem;
                        }
                    }
                    return CurLargest;
                }

                //set n to next id
                let n = LargestId()+1;
                console.log(n);

                function MakeBox(clickBtn, bId){
                    //get box element
                    //alert(bId);
                    var btn = document.getElementById(bId);
                    let curBox = btn.parentElement.parentElement;

                    //is left clicked
                    if(clickBtn == 0){
                        //get second child of box
                        let secChild = curBox.children[1];

                        //create new box div under child
                        var newBoxElm = document.createElement("div");
                        newBoxElm.className = "box";

                        //create two inn divs under new box
                        var innDiv1 = document.createElement("div");
                        var innDiv2 = document.createElement("div");
                        innDiv1.className="inn"; innDiv2.className="inn2";
                        newBoxElm.appendChild(innDiv1); newBoxElm.appendChild(innDiv2);

                        //create textarea and button with same atributes as usual under div 1
                        var newTextArea = document.createElement("div");
                        var newBtn = document.createElement("Button");
                        newTextArea.contentEditable = "true";
                        newBtn.innerHTML="";
                        newBtn.id = String(n);  //use counter as id
                        newBtn.setAttribute("onmousedown", "MakeBox(event.button, this.id)");
                        innDiv1.appendChild(newTextArea); innDiv1.appendChild(newBtn);

                        //alert(newBtn.id);

                        //asign box
                        secChild.appendChild(newBoxElm);

                        //counter +1
                        n += 1;
                        //alert("complete");
                    }
                    //otherwise right click?
                    else if(clickBtn == 2){
                        //check its not main
                        if(btn.id != "0")
                        {
                            //alert(btn.id);
                            //destroy box element
                            curBox.remove();
                        }
                    }

                }
            </script>
        </section>
    </body>
</html>
