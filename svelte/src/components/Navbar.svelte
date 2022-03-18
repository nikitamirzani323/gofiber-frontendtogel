<script>
    import moment from "moment";
    let clockmachine = "";
    function updateClock (){
        let currentTimeString = moment();
        let endtime = moment(currentTimeString).format("DD MMM YYYY | HH:mm:ss");
        clockmachine = endtime;
    }
    $: {
        setInterval(updateClock, 1000)
    }
</script>
<div class="navbar-fixed-top">
    <nav id="headernavtop" style="background:#181a20;">
        <div class="container">
            <div class="row" >
                <a href="/" title="" >
                    <img 
                        id="imglogo"
                        alt="" 
                        style="margin-top:0px;"
                        width="150" 
                        src="logo.png" />
                </a>
                <ul class="nav navbar-nav navbar-right" style="padding-right:5px;">
                    <li>
                        <div style="margin-top:8px;color:white;font-size:12px;margin-right:10px;">
                            Developer | 
                        </div>
                    </li>
                    <li>
                        <div style="margin-top:8px;color:white;font-size:12px;margin-right:10px;" ng-cloack>
                            IDR : <span style="color:#fc0;" >5.000.000</span>&nbsp;<span class="glyphicon glyphicon-refresh" style="cursor:pointer;"></span>
                        </div>
                    </li>
                </ul>
                
            </div>
        </div>
    </nav>
    <div class="clearfix"></div>
    <nav id="headernav" class="navbar navbar-default" style="background:#181a20;border-bottom:1px solid #121212;box-shadow: 0px 3px 5px -1px rgba(0, 0, 0, 0.2), 0px 6px 10px 0px rgba(0, 0, 0, 0.14), 0px 1px 18px 0px rgba(0, 0, 0, 0.12);}">
        <div class="container">
            <div class="row">
                <div class="navbar-header">
                    <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
                        <span class="sr-only">Toggle navigation</span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                    </button>
                </div>
                <div id="navbar" class="navbar-collapse collapse">
                    <ul id="headernavul" class="nav navbar-nav">
                        <li>
                            <a href="/">HOME</a>
                        </li>
                    </ul>
                    <ul class="nav navbar-nav navbar-right" style="padding-right:5px;">
                        <li style="margin-top:10px;color:#fc0;">{clockmachine}</li>
                    </ul>
                </div><!--/.nav-collapse -->
            </div>
        </div>
    </nav>
</div>
<div class="clearfix"></div>
<style>
    .navbar{
        min-height: 40px;
        max-height: 40px;
        height: 40px;
        border:1px solid #121212;
    }
    
    .navbar-nav > li > a {
        padding-top: 5px;
        padding-bottom: 12px;
        line-height: 20px;
        font-size: 15px;
        color: white;
        text-decoration: none;
    }
    #headernav{
        min-height: 35px;
        max-height: 35px;
        height: 35px;
    }
    #headernavul > li > a {
        padding-top: 5px;
        padding-bottom: 12px;
        line-height: 15px;
    }
</style>