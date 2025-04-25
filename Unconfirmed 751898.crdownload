from flask import Flask, render_template, request, redirect, url_for
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://postgres:2171@localhost/project_dbms'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)

class Guest(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    email = db.Column(db.String(100), nullable=False)
    phone = db.Column(db.String(20), nullable=True)

# Initialize the database and create tables
with app.app_context():
    db.create_all()

@app.route('/')
def index():
    guests = Guest.query.all()
    return render_template('index.html', guests=guests)

@app.route('/add_guest', methods=['POST'])
def add_guest():
    name = request.form['name']
    email = request.form['email']
    phone = request.form['phone']

    new_guest = Guest(name=name, email=email, phone=phone)
    db.session.add(new_guest)
    db.session.commit()

    return redirect(url_for('index'))

if __name__ == '__main__':
    app.run(debug=True)
