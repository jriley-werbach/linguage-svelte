<script>
    import ExploreInfo from './ExploreInfo.svelte' 
    import PhonemeBox from './PhonemeBox.svelte'
    export let selectedLanguage
</script>


<style>
    #main{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }
    h1{
        padding-left: 1rem;
    }
    h2{
        margin-left: 2rem;
        border-bottom: 3px solid black;
    }
    p{
        padding-left: 3.5rem;
    }
    #all-info-container{
        width: 50%;
        overflow: scroll;
    }
    #sounds-box{
        width: 33%;
        padding-right: 3.5rem;
        position: relative;
        bottom: 5rem;
    }
    img{
        height:4.3rem;
    }
    a{
        color: #598502 !important;
        padding-top: 1rem;
        text-decoration: none;
        font-size: 1.3rem;
    }
    a:hover{
        color: black !important;
        text-decoration: underline;
    }
    #sound-header{
        display: flex;
        justify-content: center;
        border: none;
        text-decoration: underline;
    }
</style>


<h1>{selectedLanguage.name} ({selectedLanguage.written_name})</h1>
<div id="main">
    <div id="all-info-container">
        <div id="general-info-box">
            <h2>General Information:</h2>
            <p>◦ Say Hello! : "{selectedLanguage.hello}"</p>
            <!-- This one is not a componenet due to unique use of quotes around it ^^ -->
            <ExploreInfo infoName="Number of Speakers" selectedLanguageInfo={selectedLanguage.speakers}/>
            <ExploreInfo infoName="General Language Family" selectedLanguageInfo={selectedLanguage.language_family.general_family}/>
            <ExploreInfo infoName="Specific Language Family" selectedLanguageInfo={selectedLanguage.language_family.specific_family}/>
        </div>
        <div id="grammar-info-box">
            <h2>Grammar Facts:</h2>
            <ExploreInfo infoName="Writing System" selectedLanguageInfo={selectedLanguage.orthography.name}/>
            <ExploreInfo infoName="Writing System Type" selectedLanguageInfo={selectedLanguage.orthography.system}/>
            <ExploreInfo infoName="Morphology" selectedLanguageInfo={selectedLanguage.morphology.name}/>
            <ExploreInfo infoName="Morhphology Description" selectedLanguageInfo={selectedLanguage.morphology.description}/>
            <ExploreInfo infoName="Noun Classes/Genders" selectedLanguageInfo={selectedLanguage.noun_classes}/>
            <ExploreInfo infoName="Other Features" selectedLanguageInfo={selectedLanguage.contrastive_diacritic}/>
        </div>
    </div>
    <div id="sounds-box">
    <h2 id="sound-header">Sound Inventory:</h2>
        <PhonemeBox phonemes={selectedLanguage.phonemes}/>
        {#if selectedLanguage.name === "English"}
            <a href="https://www.duolingo.com/"><img src="./media/duo_gif.gif" alt="duo owl"> Practice {selectedLanguage.name} on Duolingo!</a>
        {:else}
            <a href="https://www.duolingo.com/course/{selectedLanguage.duolingo}/en/"><img src="./media/duo_gif.gif" alt="duo owl"> Start learning {selectedLanguage.name} on Duolingo!</a>
        {/if}
    </div>
</div>