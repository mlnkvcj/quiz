<script>
    let question;
    let correctAnswer;
    let incorrectAnswers;
    import { onMount } from "svelte";
    

    const shuffle = (array) => array.sort( () => .5 - Math.random() );
    

    const handleClick = (answer) =>{
        if(answer == correctAnswer){
            alert("Tacno!")
        }
        else{
            alert(`Netačno! Tačan odgovor je ${correctAnswer}`)
        }
    }
   

    const getQuestion = async() => {
        const res = await fetch("https://opentdb.com/api.php?amount=1&difficulty=easy&type=multiple");
        let data = await res.json();
        console.log(data);
        let q;
        q.question = data.results[0].question;
        q.correctAnswer = data.results[0].correct_answer;
        q.incorrectAnswers = data.results[0].incorrect_answers;
        possibleAnswers = shuffle([...incorrectAnswers,correctAnswer]);
    }
    onMount(getQuestion)
    
</script>

<div>
    <h3>{@html question}</h3>


    <div id = "answers">
        {#each possibleAnswers as pa}
            <button on:click= {() => handleClick(pa)}>{pa}</button>
        {/each}
    </div>
</div>

