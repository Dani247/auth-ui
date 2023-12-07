<script>
    import Login from "../components/Login.svelte";

</script>

<div class="container">
    <div class="responsive-container">
        <!-- Content goes here -->
        <Login></Login>
    </div>
</div>

<style>
    .container {
        display: flex;
        justify-content: center;
        margin-top: 2rem;
    }
    /* Base styles for the container */
    .responsive-container {
        width: 100%; /* Full width by default */
        padding: 20px;
        /* background-color: lightgrey; */
        box-sizing: border-box;
    }

    /* Medium devices (tablets, 768px and up) */
    @media (min-width: 768px) {
        .responsive-container {
            width: 75%; /* Reduced width on medium devices */
        }
    }

    /* Large devices (desktops, 992px and up) */
    @media (min-width: 992px) {
        .responsive-container {
            width: 50%; /* Further reduced width on large devices */
        }
    }

    /* Extra large devices (large desktops, 1200px and up) */
    @media (min-width: 1200px) {
        .responsive-container {
            width: 25%; /* Smallest width on extra large devices */
        }
    }
</style>
