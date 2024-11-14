Passphrase is: abcd

{ symmetrically

   --
   -- the option -c encrypts a file symmetrically:
   --
   gpg -c document-to-be-encrypted-symmetrically.txt
   rm document-to-be-encrypted-symmetrically.txt

   --
   -- Decrypt the file again

   gpg -d -o document-to-be-encrypted-symmetrically.txt document-to-be-encrypted-symmetrically.txt.gpg



}
Decrypt

   
   By default, decrypts to STDOUT:

      gpg -d                 Document.txt.gpg

   Use -o to specify file:

      gpg -d -o Document.txt Document.txt.gpg

On batch

   gpg -c --batch --yes --passphrase "one two three"                      another-Document.txt

   gpg -d --batch --yes --passphrase "one two three" -o another-Document.txt2 another-Document.txt.gpg

{ Umlauts / https://superuser.com/questions/1605256/what-do-i-have-to-do-in-cmd-exe-and-or-powershell-to-specify-a-file-o-with-um?noredirect=1

   gpg -c --batch --yes --passphrase "one two three" -o bärlauch.gpg bärlauch.txt
   rm bärlauch.txt

   gpg -d --batch --yes --passphrase "one two three" -o bärlauch.txt bärlauch.gpg
#  gpg -d --batch --yes --passphrase "one two three" --enable-special-filenames -o bärlauch.txt bärlauch.gpg

   mv b*rlauch.txt bärlauch.txt
   rm bärlauch.gpg

}
{ --embedded-filename

   gpg -c --batch --yes --passphrase "one two three" --use-embedded-filename  bärlauch.txt

   rm bärlauch.txt

   gpg -d --batch --yes --passphrase "one two three" --use-embedded-filename bärlauch.txt.gpg

   mv b*rlauch.txt bärlauch.txt
   rm bärlauch.gpg
}



Show something:

   gpg --list-packets -vv --show-session-key Document.txt.gpg

Encrypt an entire directory

   gpgtar -c -o dir.pgp dir

List contents of directory

   gpgtar -t dir.pgp

Decrypt directory

   gpgtar -d      dir.pgp      (extracts to dir_1_ or so)
   gpgtar -d -C . dir.pgp      (creates dir directory directly underneath)


Show content of encrypted directory

   gpgtar --list-archive dir.pgp

Extract encrypted directory to current directory:

   gpgtar -d -C . dir.pgp

Show session key (and decrypt file)

   gpg --show-session-key Document.txt.gpg

Get someone's preferred symetric cypher
   darkcoding.net/software/how-gpg-works-encrypt/

   gpg --recv-keys 0x127CFCD9B3B929D2
