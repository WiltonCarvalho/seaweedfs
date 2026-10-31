# seaweedfs

```
cat <'EOF'> s3.json
{
  "identities": [
    {
      "name": "root",
      "credentials": [
        {
          "accessKey": "root",
          "secretKey": "root@123"
        }
      ],
      "actions": [
        "Admin",
        "Read",
        "Write",
        "List",
        "Tagging"
      ]
    }
  ]
}
EOF
```
```
docker run -it --rm --name seaweedfs \
    -v seaweed_data:/data \
    -v ./s3.json:/s3.json \
    -p 8333:8333 -p 8888:8888 -p 12535:12535 \
    --entrypoint=weed chrislusf/seaweedfs \
    mini -dir=/data -s3 -master.raftHashicorp -s3.config=/s3.json -adminUser=root -adminPassword=root@123
```
```
docker run -it --rm --entrypoint= \
  -e AWS_ACCESS_KEY_ID='root' \
  -e AWS_SECRET_ACCESS_KEY='root@123' \
  -e AWS_ENDPOINT_URL_S3='http://172.17.0.1:8333' \
  public.ecr.aws/aws-cli/aws-cli bash
```
```
aws s3 ls
aws s3 mb s3://test
echo test > test.txt
aws s3 cp test.txt s3://test/
aws s3 ls s3://test/
```
