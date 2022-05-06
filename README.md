# Naive-Bayes-in-bash
#how to suse the code
if[$#-eq 1]
then
word=$1
else
echo"usage:enron_naive_bayes.sh<word>"
  exit
  fi
  
  
  #if the file does not exist,download deom the web
  if![-e enron1.tar.gz]
  then
  wget'http://www.aueb.gr/users/ion/data/enron-spam/preprocessed/enron1.tar.gz'
  fi
  
  #if the directory does not exist, uncompress the .tar.gz
  if ![-d enron1]
  then
  tar zxvf enron1.tar.gz
  fi
  
  #change into enron1
  cd enron1
  
  #get counts of total spam,ham, and overall messages
  Nspam='ls-l spam/*.txt|wc-l'
  Nham='ls-l ham/*.txt|wc-l'
  Ntot='$Nspam+$Nham
  
  echo $Nspam spam examples
  echo $Nham ham examples
  
  #get countscontaining word in spam and ham classes
  Nword_spam='grep-il $word spam/*.txt|wc-l'
  Nword_ham'grep-il $word ham/*.txt|wc-l'
  
  echo $Nword_spam "spam examples containing $word"
  echo $Nword-ham "ham examples containing $word"
  
  #calculate probabilities using bash claculator "bc"
  Pspam='echo "scale=4;$Nspam/($Nspam+$Nham)"|bc'
  Pham='echo"scale=4;1-$Pspam"|bc'
  echo
  echo "estimated P(spam)="$Pspam
  echo "estimated P(ham)="$Pham
  
  Pword_spam='echo "scale=4;$Nword_spam/$Nspam"|bc'
  Pword_ham='echo"scale=4;$nWORD_HAM/$Nham"|bc'
  echo"estimated P($word|spam)=" $Pword_spam
  echo"estimated P($word|ham)=" $Pword_ham
  
  Pspam_word='echo "scale=4;$Pword_spam*$Pspam"|bc'
  Pham_word='echo "scale=4;$Pword_ham*$Pham"|bc'
  Pword='echo "scale=4;$Pspam_word+$Pham_word"|bc'
  Pspam_word='echo "scale=4;$Pspam_word/$Pword"|bc'
  echo
  echo"P(spam|$word)="$Pspam_word
  
  
