<template>

<div class="outerWrapper">
    <div class="innerWrapper">
        <div class="photo">
            <div class="description">
                <h2 class="title">Lorem ipsum</h2>
                    <p class="description">
                    Lorem ipsum doloro sit omet,  Lorem ipsum doloro sit omet,  Lorem ipsum doloro sit omet,
                    Lorem ipsum doloro sit omet,  Lorem ipsum doloro sit omet,  Lorem ipsum doloro sit omet,
                    Lorem ipsum doloro sit omet,  Lorem ipsum doloro sit omet,
                    </p>
            
            </div>
        </div>
</div>
</div>

</template>

<script>
export default {
    name: 'Modal',


};
</script>

<style>

.outerWrapper{
    display: none;
    background: #f6f6f6;    
    max-width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
}

.innerWrapper {
    display: flex;
    height: 100%;
    padding: 50px;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}

</style>