# How-to-count-number-of-pages
How to count number of pages in pdf or document file in php


$file ="https://tcp-salesforce.s3.amazonaws.com/letters/batch_print_1472562049_2016-08-30.pdf";
if (!$fp = @fopen($file,"r")) {
        echo 'failed opening file '.$file;
}
else {
        $max=0;
        while(!feof($fp)) {
                $line = fgets($fp,255);
                if (preg_match('/\/Count [0-9]+/', $line, $matches)){
                        preg_match('/[0-9]+/',$matches[0], $matches2);
                        if ($max<$matches2[0]) $max=$matches2[0];
                }
        }
        fclose($fp);
        echo 'There '.($max<2?'is ':'are ').$max.' page'.($max<2?'':'s').
             ' in '. $file.'.';
}
