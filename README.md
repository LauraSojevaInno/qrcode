<!DOCTYPE html>
<html>
    <head>
        <title>Coeur d'amis</title>
        <meta charset="utf-8"/>
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
        <link href="https://fonts.googleapis.com/css2?family=Cabin:wght@500&family=Krona+One&display=swap" rel="stylesheet">
    </head>
    <body>
        <?php
            $dbhost="mysql:host=laurasojrjcoeur.mysql.db;dbname=laurasojrjcoeur;charset=utf8";
            $dbuser="laurasojrjcoeur";
            $dbpass="Laura1999";
            $connexion=new PDO("$dbhost","$dbuser","$dbpass");
            $table="coeur_amis";
            $requete="SELECT * FROM $table";
            $resultat=$connexion->query($requete);
            $nombre=$resultat->rowcount();
            $flag_new=TRUE;
                if(isset($_POST['txtnom']))
                    $txtnom=$_POST['txtnom'];
                else
                    $txtnom=null;

                if(isset($_POST['txtadres']))
                    $txtadres=$_POST['txtadres'];
                else
                    $txtadres=null;

                if(isset($_POST['txtpost']))
                    $txtpost=$_POST['txtpost'];
                else
                    $txtpost=null;

                if(isset($_POST['txtgemeente']))
                    $txtgemeente=$_POST['txtgemeente'];
                else
                    $txtgemeente=null;
                
                if(isset($_POST['txtnum']))
                    $txtnum=$_POST['txtnum'];
                else
                    $txtnum=null;
                
                if(isset($_POST['txtemail']))
                    $txtemail=$_POST['txtemail'];
                else
                    $txtemail=null;
                if(isset($_POST['txtdate']))
                    $txtdate=$_POST['txtdate'];
                else
                    $txtdate=null;

                
        ?>
        <div class="jumbotron">
            <h1 class="display-4">We hebben jouw hulp nodig ! </h1>
            <p class="lead">Aanwezigheidsformulier covid-19 - Gasten HORECA</p>
            <hr class="my-4">
            <h3>Formulier</h3>
            <p>Belangrijk : één (1) persoon per tafel/boeking dient dit in te vullen.</p>
          </div>

          <form method="post" action="<?php $_SERVER['PHP_SELF'];?>">
            <div class="form-group">
              <label for="Naam">Naam</label>
              <input type="text" class="form-control" name="txtnom" value="<?php echo $txtnom; ?> " placeholder="Naam">
              <?php
                if(isset($_POST['cmdok']) && empty($txtnom))
                    {
                        echo "<b><font color=\"#FF0000\"> In te vullen </font></b>";
                        $flag_new=FALSE;
                    }
                ?>
            </div>

            <div class="form-group">
              <label for="Adres">Adres</label>
              <input type="text" class="form-control"  name="txtadres" value="<?php echo $txtadres; ?> " placeholder="Adres">
              <?php
                if(isset($_POST['cmdok']) && empty($txtadres))
                    {
                        echo "<b><font color=\"#FF0000\"> In te vullen </font></b>";
                        $flag_new=FALSE;
                    }
                ?>
            </div>

            <div class="form-group">
                <label for="Postcode">Postcode</label>
                <input type="text" class="form-control" name="txtpost" value="<?php echo $txtpost; ?>" placeholder="Postcode">
                <?php
                if(isset($_POST['cmdok']) && empty($txtpost))
                    {
                        echo "<b><font color=\"#FF0000\"> In te vullen </font></b>";
                        $flag_new=FALSE;
                    }
                ?>
            </div>

            <div class="form-group">
                <label for="Gemeente">Gemeente</label>
                <input type="text" class="form-control" name="txtgemeente" value="<?php echo $txtgemeente; ?>" placeholder="Gemeente">
                <?php
                if(isset($_POST['cmdok']) && empty($txtgemeente))
                    {
                        echo "<b><font color=\"#FF0000\"> In te vullen </font></b>";
                        $flag_new=FALSE;
                    }
                ?>
            </div>

            <div class="form-group">
                <label for="Telefoonnummer">Telefoonnummer</label>
                <input type="text" class="form-control" name="txtnum" value="<?php echo $txtnum; ?>" placeholder="Telefoonnumer">
                <?php
                if(isset($_POST['cmdok']) && empty($txtnum))
                    {
                        echo "<b><font color=\"#FF0000\"> In te vullen </font></b>";
                        $flag_new=FALSE;
                    }
                ?>
            </div>
         

            <div class="form-group">
                <label for="e-mailadres">e-mailadres</label>
                <input type="text" class="form-control" name="txtemail" value="<?php echo $txtemail; ?>" placeholder="e-mailadres">
                <?php
                if(isset($_POST['cmdok']) && empty($txtemail))
                    {
                        echo "<b><font color=\"#FF0000\"> In te vullen </font></b>";
                        $flag_new=FALSE;
                    }
                ?>         
            </div>

            <div class="form-group">
                <label for="Datum" class="col-2 col-form-label">Datum van bezoek</label>
                <input type="date" class="form-control" name="txtdate" value="<?php echo $txtdate; ?>" placeholder="Datum van bezoek">
                <?php
                if(isset($_POST['cmdok']) && empty($txtdate))
                    {
                        echo "<b><font color=\"#FF0000\"> In te vullen </font></b>";
                        $flag_new=FALSE;
                    }
                ?>
                <br>
                <p>Ik verklaar op eer geen symptomen te hebben die wijzen op COVID en geen weet te hebben dat ik
                    besmet ben met COVID en de laatste 14 dagen niet gecontacteerd te zijn door het coronacontactcenter.
                    Ik ben mij bewust van het risico dat ik neem met dit bezoek mbt mijn eigen gezondheid.</p>
                <br>
                  <center><input type="submit" name="cmdok" value="Versturen" class="site-btn"></center> 
            </div>
        </form>
        
             <br>
            <?php
                if(isset($_POST['cmdok']) && ($flag_new))
                {
                    $txtnom=strtoupper(htmlentities($_POST['txtnom']));
                    $txtadres=htmlentities($_POST['txtadres']);
                    $txtpost=htmlentities($_POST['txtpost']);
                    $txtgemeente=htmlentities($_POST['txtgemeente']);
                    $txtnum=htmlentities($_POST['txtnum']);
                    $txtemail=htmlentities($_POST['txtemail']);
                    $txtdate=htmlentities($_POST['txtdate']);
                    $reque2="INSERT INTO $table(txtnom,txtadres,txtpost,txtgemeente,txtnum,txtemail,txtdate) VALUES ('$txtnom','$txtadres','$txtpost','$txtgemeente','$txtnum','$txtemail','$txtdate')";
                    $connexion->query($reque2);
                    echo "Dank u voor uw hulp :D <br>";
                    $nombre++;
                    echo "U bent toegegvoegd";
                   
                   
                 
                    
                    
                }
            ?>
       
        <footer class="page-footer font-small blue">

        <div class="footer-copyright text-center py-3">© 2020 Copyright :
            <a href=""> ESE </a>
        
  
        </footer>

        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
    </body>
</html>
<style>
    .jumbotron{
        background-image: url("https://www.coeurdamis.be/sites/default/files/styles/gallery/public/images-src/gallery/2019-11/DSC_2236.jpg?itok=V4p42que");
        background-repeat:no-repeat;
        background-position:center;
        -webkit-background-size:cover;
        -moz-background-size:cover;
        -o-background-size:cover;
        color:#ecf0f1;
        text-align:center;
        font-size:18px;
        font-family: 'Cabin', sans-serif;
    }
    .form-group{
        width:75%;
        margin-left:auto;
        margin-right:auto;
        font-family: 'Cabin', sans-serif;
    }
    .site-btn {
    font-size: 20px;
	border-radius: 100px;
    font-family: 'Cabin', sans-serif;
    border:none;
    color:white;
    background-color:#2f3542;
    }
</style>