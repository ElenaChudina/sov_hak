aws s3 cp s3://download.tplinkcloud.com/firmware/Tapo_C200v3_en_1.4.2_Build_250313_Rel.40499n_up_boot-signed_1747894968535.bin Tapo_C200v4_en_1.4.2.bin --no-sign-request

grep -n "Failed|RSAKEY" rsa_key_extractor.log

cd ~/tp-link-decrypt
