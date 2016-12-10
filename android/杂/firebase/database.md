## firebase_database
似乎需要翻墙
![enter description here][1]
```
private static String TAG="firebase";
    private void readDatabase() {
        // Read from the database
        myRef.addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(DataSnapshot dataSnapshot) {
                // This method is called once with the initial value and again
                // whenever data at this location is updated.
                String value = dataSnapshot.getValue(String.class);
                Log.d(TAG, "Value is: " + value);
            }

            @Override
            public void onCancelled(DatabaseError error) {
                // Failed to read value
                Log.w(TAG, "Failed to read value.", error.toException());
            }
        });
    }
    private DatabaseReference myRef;
    private void initFirebaseDatabase() {
        // Write a message to the database
        FirebaseDatabase database = FirebaseDatabase.getInstance();
        myRef = database.getReference("message");
        myRef.setValue("Hello, World!");
    }
```
  [1]: ./images/1481202983971.jpg "1481202983971.jpg"