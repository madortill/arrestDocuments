<template>
    <div id="part1-documents">
        <div class="document1">
            <div class="que1">
                <input type="text" class="input 1p.n"/>
                <input type="text" class="input 1rank"/>
                <input type="text" class="input 1lastN"/>
                <input type="text" class="input 1firstN"/>
                <input type="text" class="input 1forse"/>
                <input type="text" class="input 1squad"/>
                <input type="text" class="input 1role"/>
            </div>
            <!-- <img src="@/assets/media/part1documents/arrestReport.svg" alt="arrestReport"> -->
        </div>
    </div>

</template>

<script>
</script>

<style scoped>
.document1 {
  width: 40rem;
  height: 45rem;
  background-image: url('@/assets/media/part1documents/arrestReport.svg');
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.que1 {
display: flex;
flex-direction: row;
align-items: center;

}
.input {
    position: relative;
    margin-top: 11.5rem;
    right: 9.5rem;
    width: 2.7rem;
    border: solid 2px;

}

</style>
