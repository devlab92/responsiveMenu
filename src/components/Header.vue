<template>
    <div id="nav" class="flex" :class="{ active: dropMenu }">
        <div id="navBody" class="flex">
            <div id="logo" class="flex" @click="dropMenu = !dropMenu" :class="{ logoActive: dropMenu }">
                <img class="boxRgb" src="@/assets/luiz_logo.jpeg" />
            </div>
            <div id="opts" class="flex">
                <div id="opt1">
                    <p>OPTION 1</p>
                </div>
                <div id="opt2">
                    <p>OPTION 2</p>
                </div>
                <div id="opt3">
                    <p>OPTION 3</p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>

export default {
    data() {
        return {
            dropMenu: false,
            scrollPosition: 0,
        };
    },
    created() {
        // stay ever listening the scroll moviment. If true call to function
        window.addEventListener("scroll", this.scrollMove);
    },
    methods: {
        // If scroll get more 25 or less 25 pixels the menu will be collapsed  setting dropMenu as false
        scrollMove() {
            if (this.scrollPosition + 25 < window.scrollY || this.scrollPosition - 25 > window.scrollY) {
                this.scrollPosition = window.scrollY;
                this.dropMenu = false;
            }
        },
    },
};
</script>

<style scoped>
#nav {
    position: fixed;
    top: -160px;
    width: 100%;
    height: 150px;
    background: rgba(54, 145, 197);
    margin: 0;
    align-items: center;
    transition: all 1000ms cubic-bezier(0.68, -0.55, 0.265, 1.55);
    transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.active {
    top: 0px !important;
}

#navBody {
    width: 100%;
    justify-content: space-between;
    background: rgb(51, 51, 51);
    padding: 15px 15%;
}

#logo {
    align-items: center;
}

.logoActive img {
    position: absolute;
    top: 25px !important;
    height: 100px !important;
}

#logo img {
    height: 50px;
    border-radius: 50px;
    position: fixed;
    top: 10px;
    left: 10%;
    transition: all 1000ms cubic-bezier(0.68, -0.55, 0.265, 1.55);
    transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

#logo img:hover {
    box-shadow: chartreuse 1px 1px 10px;
    cursor: pointer;
}
#opts {
    flex: 1;
    justify-content: space-evenly;
    font-weight: 200;
}

/* FOR DISPLAY MOBILE 768px  */
@media screen and (max-width: 768px) {
    #navBody {
        width: 100%;
        background: rgba(21, 99, 138, 0.562);
    }

    #logo img {
        top: 10px;
        left: 75% !important;
    }

    .logoActive img {
        height: 75px !important;
    }
    #opts {
        flex: 1;
        flex-direction: column;
        align-items: flex-start;
        font-weight: 600;
        transition: all 1000ms;
    }
}

.flex {
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>




