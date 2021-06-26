# Dice-Game

```java
public void onRoll(View v){

        starting.setText("0");
        try{
            rollingdice.release();
            count.release();
            cheer.release();
        }catch(Exception e){}

        try{
            rollingdice = MediaPlayer.create(getApplicationContext(),R.raw.dicerolling);
            rollingdice.start();
            int dicegif = getResources().getIdentifier("com.potato.mysqlproject:raw/dice"+param2.getText(),"drawable",getPackageName());
            imageView.setImageResource(dicegif);
            //Glide.with(MainActivity.this).load("http://"+MainActivity.this.getTitle()+"/game/dice.gif").into(imageView);
            final Handler handler = new Handler();
            handler.postDelayed(new Runnable() {
                @Override
                public void run() {
                    //[0,5] + 1 => [1,6]
                    final int dice1 = new Random().nextInt(7-1)+1;
                    final int dice2 = new Random().nextInt(7-1)+1;
                    final int dice3 = new Random().nextInt(7-1)+1;

                    String d = String.valueOf(dice1)+String.valueOf(dice2);
                    int sum = dice1+dice2;

                    if(param2.getText().toString().equals("3")){
                        d = String.valueOf(dice1)+String.valueOf(dice2)+String.valueOf(dice3);
                        sum = dice1+dice2+dice3;
                    }

                    int id = getResources()
                            .getIdentifier("com.potato.mysqlproject:raw/dice"+param2.getText()+d,"drawable",getPackageName());

                    imageView.setImageResource(id);

                    //if your get the image file from the internet
                    //Glide.with(MainActivity.this).load("http://"+MainActivity.this.getTitle()+"/game/dice-"+dice1+"-"+dice2+".jpg").into(imageView);
                    rollingdice.release();

                    // sound of the figure of the result
                    int s = getResources().getIdentifier("com.potato.mysqlproject:raw/j"+sum,"drawable",getPackageName());
                    count = MediaPlayer.create(getApplicationContext(),s);
                    count.start();

                    if(dice1==dice2 && sum!=12 && sum!=18 && param2.getText().toString().equals("2")){
                        cheer = MediaPlayer.create(getApplicationContext(),R.raw.congratulations);
                        cheer.start();
                    }
                    if(dice1==dice2 && dice1==dice3 && sum!=18 && param2.getText().toString().equals("3")){
                        cheer = MediaPlayer.create(getApplicationContext(),R.raw.congratulations);
                        cheer.start();
                    }
                    if((dice1==dice2 && sum==12 && param2.getText().toString().equals("2")) ||
                            (dice1==dice2 && dice1==dice3 && sum==18 && param2.getText().toString().equals("3"))
                     ){
                        cheer = MediaPlayer.create(getApplicationContext(),R.raw.yupta);
                        cheer.start();
                    }
                    gridLayout.removeAllViews();
                    //gridLayout.removeAllViewsInLayout();
                    createBoard();
                }
            },2000);
        }catch (Exception e){
            Toast.makeText(MainActivity.this, e.toString(), Toast.LENGTH_SHORT).show();
        }
    }
```
